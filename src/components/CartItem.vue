<template>
    <tr :data-id="id">
        <td class="id">{{ id }}</td>
        <td class="name">{{ name }}</td>
        <td class="price">{{ price }}</td>
        <td class="qty">
            <button @click="childDecrease(id)"> - </button>
            {{ qty }}
            <button @click="childIncrease(id)"> + </button>
        </td>
        <td class="sub">{{ qty * price }}</td>
        <td><span class="del" @click="childRemoveFromCart(id)"><img src="images/trash.gif"></span></td>
    </tr>
</template>

<script>
import { bus } from '../main'
export default {
    props: {
        id: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        price: {
            type: Number,
            required: true
        },
        qty: {
            type: Number,
            required: true
        }
    },
    methods: {
        childRemoveFromCart(id) {
            bus.$emit('remove-from-cart', id)
        },
        childDecrease(id) {
            bus.$emit('item-decrease', id)
        },
        childIncrease(id) {
            bus.$emit('item-increase', id)
        }
    }
}
</script>