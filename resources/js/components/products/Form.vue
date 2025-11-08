<script setup>
 import { reactive } from 'vue'


 const form = reactive({
    name: "",
    description: "",
    image: "",
    type: "",
    quantity: "",
    price: ""

 })

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

 const handleSave = () => {
    axios.post('/api/products', form)
 }

</script>


<template>
            <section>
            <div class="titlebar">
                <h1>Create Product</h1>
                <button @click="handleSave">Save</button>
            </div>
            <div class="card">
                <div>
                    <label>Name</label>
                    <input type="text" v-model="form.name">
                    <label>Description (optional)</label>
                    <textarea cols="10" rows="5" v-model="form.description"></textarea>
                    <label>Add Image</label>
                    <img :src="getImage()" alt="" class="img-product" />
                    <input type="file" @change="handleFileChange">
                </div>
                <div>
                    <label>Category</label>
                    <input type="text" v-model="form.type">
                    <hr>
                    <label>Inventory</label>
                    <input type="text" class="input" v-model="form.quantity">
                    <hr>
                    <label>Price</label>
                    <input type="text" class="input" v-model="form.price">
                </div>
            </div>
            <div class="titlebar">
                <h1></h1>
                <button @click="handleSave">Save</button>
            </div>
        </section>
</template>