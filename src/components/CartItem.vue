<template>
    <tr :data-id="id">
        <td class="id">{{ id }}</td>
        <td class="name">{{ name }}</td>
        <td class="price">{{ price }}</td>
        <td class="qty">
            <button @click="decrease(id)"> - </button>
            {{ qty }}
            <button @click="increase(id)"> + </button>
        </td>
        <td class="sub">{{ qty * price }}</td>
        <td><span class="del" @click="removeFromCart(id)"><img src="images/trash.gif"></span></td>
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
        removeFromCart(id) {
            if (confirm("Delete this item?")) {
                let target = data.cart.findIndex(function (obj, idx, ary) {
                    return obj.id === id
                })
                data.cart.splice(target, 1)
                vm.updateStorage()
            }
        },
        decrease(id) {
            let target = data.cart.findIndex(function (obj, idx, ary) {
                return obj.id === id
            })
            if (data.cart[target].qty > 1) {
                data.cart[target].qty = data.cart[target].qty - 1
            }
            vm.updateStorage()
        },
        increase(id) {
            let target = data.cart.findIndex(function (obj, idx, ary) {
                return obj.id === id
            })
            data.cart[target].qty = data.cart[target].qty + 1
            vm.updateStorage()
        }
    }
}
</script>