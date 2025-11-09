<script setup>
 import { onMounted, reactive, ref } from 'vue'
 import { useRouter, useRoute } from 'vue-router'


 const form = reactive({
    name: "",
    description: "",
    image: "",
    type: "",
    quantity: "",
    price: ""

 })

 const router = useRouter()

 const route = useRoute()

 let errors = ref([])

 const editMode = ref(false)

 onMounted(() =>{
    if(route.name === 'products.edit'){
        editMode.value = true
        getProduct()
    }
 })

 const getProduct = async () => {
    let response = await axios.get(`/api/products/${route.params.id}/edit`)
    .then((response) => {
        form.name = response.data.product.name
        form.description = response.data.product.description
        form.image = response.data.product.image
        form.type = response.data.product.type
        form.quantity = response.data.product.quantity
        form.price = response.data.product.price
    })
 }

 const getImage = () => {
    let image = "/upload/no-image.png"
    if (form.image){
        if(form.image.indexOf("base64") != -1){
            image = form.image
        }else{
            image = "/upload" + form.image
        }
    }
    return image

 }

 const handleFileChange = (e) => {
    let file = e.target.files[0]
    let reader = new FileReader()
    reader.onloadend = (file) => {
        form.image = reader.result
    }
    reader.readAsDataURL(file)
 }

 const handleSave = (values, actions) => {

    if(editMode.value){
      updateProduct(values, actions)
    }else{
      createProduct(values, actions)
    }    

 }

 const createProduct = (values, actions) => {
   axios.post('/api/products', form)
    .then((response)=>{
        router.push('/')
        toast.fire({ icon: "success", title: "Produto salvo com sucesso"})
    })
    .catch((error) =>{
        if(error.response.status === 422){
            errors.value = error.response.data.errors
        }
    })
 }

 const updateProduct = (values, actions) => {
       axios.put(`/api/products/${route.params.id}`, form)
    .then((response)=>{
        router.push('/')
        toast.fire({ icon: "success", title: "Produto atualizado com sucesso"})
    })
    .catch((error) =>{
        if(error.response.status === 422){
            errors.value = error.response.data.errors
        }
    })
 }

</script>


<template>
            <section>
            <div class="titlebar">
                <h1>
                    <span v-if="editMode">Editar</span>
                    <span v-else>Adiconar</span> 
                    Produto</h1>
                
            </div>
            <div class="card">
                <div>
                    <label>Nome</label>
                    <input type="text" v-model="form.name">
                    <small style="color:red" v-if="errors.name">{{ errors.name }}</small>
                    <label>Descrição (optional)</label>
                    <textarea cols="10" rows="5" v-model="form.description"></textarea>
                    <small style="color:red" v-if="errors.description">{{ errors.description }}</small>
                    <label>Adicionar Imagem</label>
                    <img :src="getImage()" alt="" class="img-product" />
                    <input type="file" @change="handleFileChange">
                </div>
                <div>
                    <label>Categoria</label>
                    <input type="text" v-model="form.type">
                    <hr>
                    <label>Inventário</label>
                    <input type="text" class="input" v-model="form.quantity">
                    <hr>
                    <label>Preço</label>
                    <input type="text" class="input" v-model="form.price">
                </div>
            </div>
            <div class="titlebar">
                <h1></h1>
                <button @click="handleSave">Salvar</button>
            </div>
        </section>
</template>