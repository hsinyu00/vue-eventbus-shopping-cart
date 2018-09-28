<template>
    <div class="item">
        <img :src="image" class="prod-img">
        <p>{{ id }}</p>
        <p>{{ name }}</p>
        <p>{{ price }}</p>
        <button class="add-to-cart" data-id="id" @click="childAddToCart">Add to cart</button>
    </div>
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
        image: {
            type: String,
            required: true
        }
    },
    methods: {
        childAddToCart() {
            this.$emit('add-to-cart')
        }
    }
}
</script>

<style lang="scss">
    .prod-img {
        float: left;
        margin-right: 20px;
        width: 200px;
        height: 200px;
    }
    .item {
        border-bottom: 1px solid #eee;
    }
    .item:before, .item:after {
        content: " ";
        display: table;
    }
    .item:after {
        clear: both;
    }
</style>