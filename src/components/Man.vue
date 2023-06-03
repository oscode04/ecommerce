<template>
   <div class="container">
    <!-- untuk background -->
    <div :class="switchBg">
    <!-- card -->
    <div class="card">
        <!-- gambar 404 -->
        <div :class="SwitchUnavail">
            <img src="../assets/not_available/sad-face.png" alt="">
        </div>
        <!-- gambar product -->
        <div :class="switchProducFoto">
            <img :src="product.image" alt="">
        </div>
        <!-- deskripsi product -->
        <div class="description">
            <!-- judul product -->
            <h1 :class="switchTittle">{{product.title}}</h1>
            <div :class="switchCategory">
                <!-- kategori produk -->
                <p>{{product.category}}</p>
                <!-- rating -->
                <div>
                    <div class="rating" v-if="product.rating.rate <= 2.9">
                        <p>{{product.rating.rate}}/5</p>
                        <div :class="SwitcRatFull" class="circle"></div>
                        <div :class="SwitcRatFull" class="circle"></div>
                        <div :class="SwitchRatBorder " class="circle"></div>
                        <div :class="SwitchRatBorder " class="circle"></div>
                        <div :class="SwitchRatBorder " class="circle"></div>
                    </div>
                    <div class="rating" v-else-if="product.rating.rate <= 3.9">
                        <p>{{product.rating.rate}}/5</p>
                        <div :class="SwitcRatFull" class="circle"></div>
                        <div :class="SwitcRatFull" class="circle"></div>
                        <div :class="SwitcRatFull " class="circle"></div>
                        <div :class="SwitchRatBorder " class="circle"></div>
                        <div :class="SwitchRatBorder " class="circle"></div>
                    </div>
                    <div class="rating" v-else>
                        <p>{{product.rating.rate}}/5</p>
                        <div :class="SwitcRatFull" class="circle"></div>
                        <div :class="SwitcRatFull" class="circle"></div>
                        <div :class="SwitcRatFull " class="circle"></div>
                        <div :class="SwitcRatFull " class="circle"></div>
                        <div :class="SwitchRatBorder " class="circle"></div>
                    </div>
                </div>
            </div>
            <!-- garis 1 -->
            <hr :class="SwitchLine">
            <p :class="SwitchProDes">
                {{product.description}}
            </p>
            <!-- garis 2 -->
            <hr :class="SwitchLine">
            <!-- harga -->
            <p :class="SwitchProdPrice">
               ${{product.price}}
            </p>
            <!-- khusus not avail -->
            <p :class="SwitchSorryMsg">This product is unavailable to show</p>
            <!-- button -->
            <div>
                <button :class="switchBtnBuy">
                    Buy now
                </button>
                <button @click="nextProduct" :class="switchBtnNext">
                    Next product
                </button>
            </div>
        </div>
    </div>
    <!-- end-card -->
   </div>
   </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ManPages',
  data(){
    return {
        product: {
            category: '',
            rating: {}
        },
        currentProductId: 1,
        // currentProductCategory: ``
    }
  },
  created() {
        this.getProduct(this.currentProductId)
    },
  methods: {
    getProduct(id){
        axios.get(`https://fakestoreapi.com/products/${id}`)
        .then(response => {
            // Proses response dari API
            this.product = response.data
            console.log(response.data, response.data.category);
        })
        .catch(error => {
            // Tangani kesalahan permintaan API
            console.error(error);
        });
    },
    nextProduct() {
        if(this.currentProductId == 20 ){
            this.currentProductId = 1
        } else {
            this.currentProductId += 1;
            this.getProduct(this.currentProductId);
        }
    }
  },
  computed: {
    switchBg() {
            if (this.product.category === "men's clothing") {
                return 'background'
            } else if (this.product.category === "women's clothing"){
                return 'background-w'
            } else {
                return 'background-n'
            }
    },
    switchTittle() {
            if (this.product.category === "men's clothing") {
                return 'tittle'
            } else if (this.product.category === "women's clothing"){
                return 'tittle-w'
            } else {
                return 'tittle-n'
            }
    },
    switchBtnBuy() {
            if (this.product.category === "men's clothing") {
                return 'btn-buy'
            } else if (this.product.category === "women's clothing"){
                return 'btn-buy-w'
            } else {
                return 'btn-buy-n'
            }
    },
    switchBtnNext() {
            if (this.product.category === "men's clothing") {
                return 'btn-next'
            } else if (this.product.category === "women's clothing"){
                return 'btn-next-w'
            } else {
                return 'btn-next-n'
            }
    },
    switchProducFoto(){
        if (this.product.category === "men's clothing") {
                return 'product-foto'
            } else if (this.product.category === "women's clothing"){
                return 'product-foto'
            } else {
                return 'product-foto-n'
            }
    },
    switchCategory(){
        if (this.product.category === "electronics" || this.product.category === "jewelery") {
                return 'category-n'
            } else {
                return 'category'
            }
    },
    SwitchProDes(){
         if (this.product.category === "electronics" || this.product.category === "jewelery") {
                return 'product-description-n'
            } else {
                return 'product-description'
            }
    },
    SwitchLine(){
        if (this.product.category === "electronics" || this.product.category === "jewelery") {
                return 'line-n'
            } else {
                return 'line'
            }
    },
    SwitchProdPrice(){
         if (this.product.category === "men's clothing") {
                return 'product-price'
            } else if (this.product.category === "women's clothing"){
                return 'product-price-w'
            } else {
                return 'product-price-n'
            }
    },
    SwitchSorryMsg(){
        if (this.product.category === "electronics" || this.product.category === "jewelery") {
                return 'sorry-msg-n'
            } else {
                return 'sorry-msg'
            }
    },
    SwitchUnavail(){
        if (this.product.category === "electronics" || this.product.category === "jewelery") {
                return 'unavail-n'
            } else {
                return 'unavail'
            }
    },
    SwitcRatFull() {
        if (this.product.category === "men's clothing") {
                return 'rat-full'
            } else {
                return 'rat-full-w'
            } 
    },
    SwitchRatBorder() {
        if (this.product.category === "men's clothing") {
                return 'rat-border'
            } else {
                return 'rat-border-w'
            } 
    }
  }
}
</script>

<style>
@import url(../assets/style/style.css);
@import url(../assets/style/style2.css);
@import url(../assets/style/style3.css);
</style>