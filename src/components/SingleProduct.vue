<template>
  <div class="my-10">
    <div class="container mx-auto">
      <div class="bg-white rounded-lg p-12 w-4/6">
        <h1 class="text-2xl font-semibold mb-2">
          {{ allProducts[curID].title }}
        </h1>
        <p class="text-gray-400 text-xs">
          Артикул: {{ allProducts[curID].article }}
        </p>
        <div class="flex items-start justify-between w-full">
            <div class="w-2/5 mt-7">
                <img v-if="Clicked === false" class="w-full mainProductDisplay" ref="mainProductDisplay" :src="allProducts[curID].images[0].first"  alt="">
                <img v-if="Clicked === true" class="w-full mainProductDisplay" ref="mainProductDisplay" :src="CurDisplay"  alt="">
                <div class="flex justify-center items-center w-full">
                  <div @click="SetActiveImage(1, allProducts[curID].images[0].first)" ref="productImg" class="border-2 border-gray-400 rounded-md p-1 mr-2" :class="{ selectedImage: FirstIsActive }">
                    <img class="w-12" :src="allProducts[curID].images[0].first"  alt="">
                  </div>
                  <div @click="SetActiveImage(2, allProducts[curID].images[0].second)" ref="productImg" class="border-2 border-gray-400 rounded-md p-1 mr-2" :class="{ selectedImage: SecondIsActive }">
                    <img class="w-12" :src="allProducts[curID].images[0].second"  alt="">
                  </div>
                  <div @click="SetActiveImage(3, allProducts[curID].images[0].third)" ref="productImg" class="border-2 border-gray-400 rounded-md p-1 mr-2" :class="{ selectedImage: ThirdIsActive }">
                    <img class="w-12" :src="allProducts[curID].images[0].third"  alt="">
                  </div>
                </div>
            </div>
            <div class="w-3/5">
                <p class="bg-credit w-max p-0 text-white font-semibold rounded-sm px-1">0 - 0 - 12</p>
                <h2 class="text-xl font-semibold mt-2">Описание</h2>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Модельный год</p>
                    <p>{{ allProducts[curID].year }}</p>
                </div>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Диагональ дисплея, дюйм</p>
                    <p>{{ allProducts[curID].diagonal }}</p>
                </div>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Разрешение дисплея</p>
                    <p>{{ allProducts[curID].resolution }}</p>
                </div>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Тип матрицы</p>
                    <p>{{ allProducts[curID].matrix }}</p>
                </div>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Частота обновления</p>
                    <p>{{ allProducts[curID].hz }}</p>
                </div>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Объем оперативной памяти, ГБ</p>
                    <p>{{ allProducts[curID].ram }}</p>
                </div>
                <div class="flex justify-between items-center border-b border-dashed border-gray-300 my-2">
                    <p>Объем встроенной памяти, ГБ</p>
                    <p>{{ allProducts[curID].hard }}</p>
                </div>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
export default {
  data() {
    return {
      curID: this.$route.params.id - 1,
      FirstIsActive: true,
      SecondIsActive: false,
      ThirdIsActive: false,
      CurDisplay: null,
      Clicked: false
    };
  },
  methods: {
    ...mapActions(["fetchProducts"]),
    async SetActiveImage(id, src) {
        console.error("clicked at image");
        this.FirstIsActive = false;
        this.SecondIsActive = false;
        this.ThirdIsActive = false;    
        if (id == 1) {
          this.FirstIsActive = true
        } else if (id == 2) {
          this.SecondIsActive = true;
        } else {
          this.ThirdIsActive = true;  
        }   
        this.CurDisplay = src;
        this.Clicked = true;
    }
    },
  async mounted() {
    this.fetchProducts();
  },
  computed: mapGetters(["allProducts"]),
};
</script>