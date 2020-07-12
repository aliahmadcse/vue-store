<template>
    <div id="app" class="container mt-5">
        <router-view
            :cart="cart"
            :cartQty="cartQty"
            :cartTotal="cartTotal"
            :sliderStatus="sliderStatus"
            :maximum.sync="maximum"
            :products="products"
            @delete="deleteItem"
            @add="addItem"
            @toggle="toggleSliderStatus"
        ></router-view>
    </div>
</template>

<script>
export default {
    name: "app",

    data: function() {
        return {
            maximum: 99,
            sliderStatus: true,
            cart: [],
            products: [
                {
                    id: 1,
                    imgUrl:
                        "https://guesseu.scene7.com/is/image/GuessEU/M63H24W7JF0-L302-ALTGHOST?wid=1500&fmt=jpeg&qlt=80&op_sharpen=0&op_usm=1.0,1.0,5,0&iccEmbed=0",
                    name: "CHECK PRINT SHIRT",
                    price: 110
                },
                {
                    id: 2,
                    imgUrl:
                        "https://guesseu.scene7.com/is/image/GuessEU/FLGLO4FAL12-BEIBR?wid=700&amp;fmt=jpeg&amp;qlt=80&amp;op_sharpen=0&amp;op_usm=1.0,1.0,5,0&amp;iccEmbed=0",
                    name: "GLORIA HIGH LOGO SNEAKER",
                    price: 91
                },
                {
                    id: 3,
                    imgUrl:
                        "https://guesseu.scene7.com/is/image/GuessEU/HWVG6216060-TAN?wid=700&amp;fmt=jpeg&amp;qlt=80&amp;op_sharpen=0&amp;op_usm=1.0,1.0,5,0&amp;iccEmbed=0",
                    name: "CATE RIGID BAG",
                    price: 94.5
                },
                {
                    id: 4,
                    imgUrl:
                        "http://guesseu.scene7.com/is/image/GuessEU/WC0001FMSWC-G5?wid=520&fmt=jpeg&qlt=80&op_sharpen=0&op_usm=1.0,1.0,5,0&iccEmbed=0",
                    name: "GUESS CONNECT WATCH",
                    price: 180.9
                },
                {
                    id: 5,
                    imgUrl:
                        "https://guesseu.scene7.com/is/image/GuessEU/AW6308VIS03-SAP?wid=700&amp;fmt=jpeg&amp;qlt=80&amp;op_sharpen=0&amp;op_usm=1.0,1.0,5,0&amp;iccEmbed=0",
                    name: "'70s RETRO GLAM KEFIAH",
                    price: 20
                }
            ]
        };
    },
    computed: {
        cartTotal: function() {
            let sum = 0;
            for (let key in this.cart) {
                sum = sum + this.cart[key].product.price * this.cart[key].qty;
            }
            return sum;
        },
        cartQty: function() {
            let qty = 0;
            for (let key in this.cart) {
                qty = qty + this.cart[key].qty;
            }
            return qty;
        }
    },
    methods: {
        toggleSliderStatus: function() {
            this.sliderStatus = !this.sliderStatus;
        },
        deleteItem: function(id) {
            if (this.cart[id].qty > 1) {
                this.cart[id].qty--;
            } else {
                this.cart.splice(id, 1);
            }
        },
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