<template>
  <div id="app">
        <h2>Products</h2>
        <div id="products">
            <Product
                :id="item.id"
                :name="item.name"
                :price="item.price"
                :image="item.image"
                v-for="item in products"
                :key="item.id" @add-to-cart="addToCart(item.id)">
            </Product>
        </div>
        <h2>My Shopping Cart</h2>
        <div id="cart">
            <div v-if="cart.length > 0">
                <table>
                    <tr>
                        <th>ID</th>
                        <th>Product Name</th>
                        <th>Price</th>
                        <th>Quantity</th>
                        <th>Subtotal</th>
                        <th>Del</th>
                    </tr>
                    <!-- 這邊要用 is，否則 component 會被踢到 <table> 外面
                     https://cn.vuejs.org/v2/guide/components.html#%E8%A7%A3%E6%9E%90-DOM-%E6%A8%A1%E6%9D%BF%E6%97%B6%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9 -->
                    <tr is="cart-item" v-for="(item) in cart"
                            :key="item.src"
                            :id="item.id"
                            :name="item.name"
                            :price="item.price"
                            :qty="item.qty">
                    </tr>
                    <tr>
                        <td colspan="6">Total: {{ total }}</td>
                    </tr>
                </table>
            </div>
            <div v-else>No item in cart.</div>
        </div>
        <button id="emptyCart" @click="emptyCart">clear cart</button>
    </div>
</template>

<script>

import axios from 'axios'
import CartItem from '@/components/CartItem'
import Product from '@/components/Product'

export default {
data() {
    return {
        products: null,
        cart: []
    }
},

methods: {
    loadProducts() {
        axios({
            method: 'get',
            url: 'data/products2.json',
        })
        .then((response) => {
            let res = response.data
            this.products = res.products
        })
    },
    addToCart(id) {
        if(this.cart.length > 0) {
            let inCart = false
            // 逐條比對是否已有此商品
            for (i = 0; i < this.cart.length; i++) {
                if (this.cart[i].id === id) {
                    inCart = true;  // in cart 就不要再跑迴圈，否則會把不是這一回合的也加上去
                    this.cart[i].qty = this.cart[i].qty + 1
                    break
                }
            }
            if(!inCart) {
                let newItem = this.products.find(function (obj) { return obj.id === id; });
                newItem.qty = 1
                this.cart.push(newItem)
            }
        } else {
            let newItem = this.products.find(function (obj) { return obj.id === id; });
            newItem.qty = 1
            this.cart.push(newItem)
        }
        // this.updateStorage()
    },
    emptyCart() {
        this.cart = []
        // this.updateStorage()
    },
    updateStorage() {
        localStorage['cart'] = JSON.stringify(this.cart)
    }
},
computed: {
    total() {
        let total = this.cart.map(function(obj) {
            let sub = obj.price * obj.qty
            return sub
        }).reduce(function(result, sub) {
            return result + sub
        })
        return total
    }
},
components: {
    CartItem,
    Product
},
created() {
    this.loadProducts()
    // this.cart = JSON.parse(localStorage['cart']) || []
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
