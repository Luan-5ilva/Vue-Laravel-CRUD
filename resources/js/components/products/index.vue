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
                <h1>Produtos</h1>
                <button @click="newProduct">Adicionar Produto</button>
            </div>
            <div class="table">
                <div class="table-filter">
                    <div>
                        <ul class="table-filter-list">
                            <li>
                                <p class="table-filter-link link-active">Todos</p>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="table-search">
                    <div>
                        <button class="search-select">
                            Busca
                        </button>
                        <span class="search-select-arrow">
                            <i class="fas fa-caret-down"></i>
                        </span>
                    </div>
                    <div class="relative">
                        <input class="search-input" type="text" placeholder="Procurar produto...">
                    </div>
                </div>
                <div class="table-product-head">
                    <p>Imagem</p>
                    <p>Nome</p>
                    <p>Categoria</p>
                    <p>Estoque</p>
                    <p>Ações</p>
                </div>
                <div class="table-product-body" v-for="product in products" :key="product.id">
                    <img :src="ourImage(product.image)" />
                    <p> {{product.name}}</p>
                    <p>{{product.type}}</p>
                    <p>{{product.quantity}}</p>
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