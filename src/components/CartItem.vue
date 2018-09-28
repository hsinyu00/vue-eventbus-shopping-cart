<template>
    <tr :data-id="id">
        <td class="id">{{ id }}</td>
        <td class="name">{{ name }}</td>
        <td class="price">{{ price }}</td>
        <td class="qty">
            <button @click="childDecrease"> - </button>
            {{ qty }}
            <button @click="childIncrease"> + </button>
        </td>
        <td class="sub">{{ qty * price }}</td>
        <td><span class="del" @click="childRemoveFromCart"><img src="images/trash.gif"></span></td>
    </tr>
</template>

<script>
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
        childRemoveFromCart() {
            this.$emit('remove-from-cart')
        },
        childDecrease() {
            this.$emit('item-decrease')
        },
        childIncrease() {
            this.$emit('item-increase')
        }
    }
}
</script>