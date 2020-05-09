<template>
    <div id="app" class="container mt-5">
        <h1>My Shop</h1>
        <product-list :maximum="maximum" :products="products" @add="addItem"></product-list>
    </div>
</template>

<script>
// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "./components/ProductList.vue";

export default {
    name: "App",
    components: {
        // FontAwesomeIcon,
        ProductList
    },
    data: function() {
        return {
            maximum: 99,
            cart: [],
            products: null
        };
    },
    mounted: function() {
        fetch("https://hplussport.com/api/products/order/price")
            .then(response => response.json())
            .then(data => {
                this.products = data;
            });
    },

    methods: {
        /**
         * Method to add an item in the cart,
         * Looks, whether the item already exist, if yes, it increment
         * the quantity
         * @param product
         * @returns void
         */
        addItem: function(product) {
            var whichProduct;
            var existing = this.cart.filter(function(item, index) {
                if (item.product.id == Number(product.id)) {
                    whichProduct = index;
                    return true;
                } else {
                    return false;
                }
            });

            if (existing.length) {
                this.cart[whichProduct].qty++;
            } else {
                this.cart.push({ product: product, qty: 1 });
            }
        }
    }
};
</script>