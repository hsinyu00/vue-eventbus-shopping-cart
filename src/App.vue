<template>
  <div id="app">
        <h2>Products</h2>
        <products></products>
        <h2>My Shopping Cart</h2>
        <cart></cart>
        <!-- <button id="emptyCart" @click="emptyCart">clear cart</button> -->
    </div>
</template>

<script>

import Vue from 'vue'
import axios from 'axios'
import CartItem from '@/components/CartItem'
import Product from '@/components/Product'
import {mapGetters} from 'vuex';
import {mapActions} from 'vuex';

export default {

methods: {

},

// methods: {


    // removeFromCart(id) {
    //     if (confirm("Delete this item?")) {
    //         // https://gist.github.com/scottopolis/6e35cf0d53bae81e6161662e6374da04
    //         let target = this.cart.map(function(item) { return item.id; }).indexOf(id)
    //         this.cart.splice(target, 1)
    //         this.updateStorage()
    //     }
    // },
    // decrease(id) {
    //     let target = this.cart.map(function(item) { return item.id; }).indexOf(id)
    //     if (this.cart[target].qty > 1) {
    //         this.cart[target].qty = this.cart[target].qty - 1
    //         Vue.set(this.cart, target, this.cart[target])
    //     }
    //     this.updateStorage()
    // },
    // increase(id) {
    //     let target = this.cart.map(function(item) { return item.id; }).indexOf(id)
    //     this.cart[target].qty = this.cart[target].qty + 1
    //     Vue.set(this.cart, target, this.cart[target])

    //     this.updateStorage()
    // },
    // emptyCart() {
    //     this.cart = []
    //     this.updateStorage()
    // },
    // updateStorage() {
    //     localStorage['cart'] = JSON.stringify(this.cart)
    // }
// },
// computed: {
//     total() {
//         if(this.cart.length > 0) {
//             let total = this.cart.map(function(obj) {
//                 let sub = obj.price * obj.qty
//                 return sub
//             }).reduce(function(result, sub) {
//                 return result + sub
//             })
//             return total
//         } else {
//             return 0
//         }
//     }
// },
    components: {
        'cart': CartItem,
        'products': Product
    },
    created() {
        this.$store.dispatch('loadProducts')
    }
}

</script>

<style lang="scss">
    table,th,td {
        border:1px solid #aaa;
    }
    #emptyCart {
        margin-top: 20px;
    }
    td {
        padding: 5px;
    }
    [v-cloak] {
    display: none;
    }
</style>
