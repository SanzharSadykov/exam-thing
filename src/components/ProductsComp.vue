<template>
    <div class="my-5 flex items-start justify-between flex-wrap">
        <div @click="$router.push({name: 'single', params: { id: product.id }})" class="bg-white singleBlock m-2 p-2" v-for="product of allProducts" :key="product.id">
            <img :src="product.images[product.id - 1].first" alt="">
            <p class="font-semibold"> {{ product.title }} </p>
            <p class="text-2xl font-semibold"> {{ product.price }} тг.</p>
        </div>
    </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
    name: "ProductsComp",
    computed: mapGetters(['allProducts']),
    async mounted() {
        this.fetchProducts()
    },
    methods: mapActions(['fetchProducts'])
}
</script>