<template>
    <div>
        <button class="btn btn-primary" @click="goBack">&laquo; Back</button>
        <h1>{{ product.name }}</h1>

        <ul class="nav nav-pills">
            <li class="nav-item">
                <router-link class="nav-link" :to="{name:'viewProduct', params: { productId: productId}}" active-class="active">Details</router-link>
            </li>
            <li class="nav-item">
                <router-link class="nav-link" :to="{name:'productReviews', params: { productId: productId}}" active-class="active">Reviews</router-link>
            </li>
        </ul>

        <hr>
        <router-view></router-view>

    </div>
</template>

<script>
import { products } from "./../data/products";
export default {
    props: {
        productId: {
            required: true
        }
    },
    data() {
        return {
            products: products,
            product: null,
            discount: 0
        };
    },
    created() {
        this.product = this.getProduct(this.productId);
    },
    watch: {
        productId(newValue) {
            this.product = this.getProduct(newValue);
        }
    },
    methods: {
        getProduct(productId) {
            let match = null;
            this.products.forEach(function(product) {
                if (product.id == productId) {
                    match = product;
                }
            });
            return match;
        },
        goBack() {
            this.$router.go(-1);
        }
    }
};
</script>