<script setup>
 import { onMounted, ref, watch } from 'vue'
 import { useRouter } from 'vue-router'


 const router = useRouter()

 let products = ref([])

 let links = ref([])

 let searchQuery = ref('')

 onMounted(async () => {
    getProducts()
 })

 watch(searchQuery, () =>{
    getProducts()
 })
 

 const newProduct = () => {
    router.push('/products/create')

 }
 
 const ourImage = (img) => {
    return "/upload/"+img
 }

 const getProducts = async () => {
    let response = await axios.get ('/api/products?&searchQuery='+searchQuery.value)
     .then((response) => {
        products.value = response.data.products.data
        links.value = response.data.products.links
    })
 }

 const changePage = (link) => {

    if(!link.url || link.active){
        return
    }

    axios.get(link.url)
     .then((response) => {
        products.value = response.data.products.data
        links.value = response.data.products.links
     })
 }

 const onEdit = (id) => {
    router.push(`/products/${id}/edit`)
 }

 const deleteProduct = (id) =>{
   Swal.fire({
         title: "Tem certeza?",
         text: "Você não poderá reverter essa decisão!",
         icon: "warning",
         showCancelButton: true,
         confirmButtonColor: "#3085d6",
         cancelButtonColor: "#d33",
         confirmButtonText: "Sim, apagar!",
         cancelButtonText: "Cancelar"
    }).then((result) => {
    if (result.isConfirmed) {
        axios.delete(`/api/products/${id}`)
         .then(() =>{
           Swal.fire({
            title: "Excluído!",
            text: "Seu arquivo foi excluído.",
            icon: "success"
            });
            getProducts()
         })
    }
    });
 }

 function formatLabel(label) {
  if (label.includes('Previous')) return '<'
  if (label.includes('Next')) return '>'
  return label
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
                        <input class="search-input" type="text" placeholder="Procurar produto..." v-model="searchQuery">
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
                        <button class="btn btn-success" @click="onEdit(product.id)">
                            <i class="fas fa-pencil-alt"></i>
                        </button>
                        <button class="btn btn-danger" @click="deleteProduct(product.id)">
                            <i class="far fa-trash-alt"></i>
                        </button>
                    </div>
                </div>
                <div class="table-paginate">
                    <div class="pagination">
                    <a 
                    href="#"    
                    class="btn"
                    v-for="(link, index) in links"
                    :key="index"
                    v-html="formatLabel(link.label)"
                    :class="{ active: link.active, disable: !link.url }"
                    @click="changePage(link)"
                    ></a>

           
                    </div>
                </div>
            </div>
        </section>
</template>