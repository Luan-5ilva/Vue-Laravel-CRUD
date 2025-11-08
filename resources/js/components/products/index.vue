<script setup>
 import { onMounted, ref } from 'vue'
 import { useRouter } from 'vue-router'


 const router = useRouter()

 let products = ref([])

 onMounted(async () => {
    getProducts()
 })
 

 const newProduct = () => {
    router.push('/products/create')

 }
 
 const ourImage = (img) => {
    return "/upload/"+img
 }

 const getProducts = async () => {
    let response = await axios.get ('/api/products')
     .then((response) => {
        products.value = response.data.products
    })
 }

</script>

<template>
            <section>
            <div class="titlebar">
                <h1>Products</h1>
                <button @click="newProduct">Add Product</button>
            </div>
            <div class="table">
                <div class="table-filter">
                    <div>
                        <ul class="table-filter-list">
                            <li>
                                <p class="table-filter-link link-active">All</p>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="table-search">
                    <div>
                        <button class="search-select">
                            Search Product
                        </button>
                        <span class="search-select-arrow">
                            <i class="fas fa-caret-down"></i>
                        </span>
                    </div>
                    <div class="relative">
                        <input class="search-input" type="text" placeholder="Search product...">
                    </div>
                </div>
                <div class="table-product-head">
                    <p>Image</p>
                    <p>Name</p>
                    <p>Category</p>
                    <p>Inventory</p>
                    <p>Actions</p>
                </div>
                <div class="table-product-body" v-for="product in products" :key="product.id">
                    <img :src="ourImage(product.image)" />
                    <p> Product name</p>
                    <p>Category</p>
                    <p>Inventory</p>
                    <div>
                        <button class="btn btn-success">
                            <i class="fas fa-pencil-alt"></i>
                        </button>
                        <button class="btn btn-danger">
                            <i class="far fa-trash-alt"></i>
                        </button>
                    </div>
                </div>
                <div class="table-paginate">
                    <div class="pagination">
                        <a href="#" disabled>&laquo;</a>
                        <a class="active-page">1</a>
                        <a>2</a>
                        <a>3</a>
                        <a href="#">&raquo;</a>
                    </div>
                </div>
            </div>
        </section>
</template>