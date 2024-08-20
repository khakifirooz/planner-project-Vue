<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input v-model="title" type="text">
    <label>Details</label>
    <textarea v-model="details"></textarea>
    <button>Update Product</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return{
            title: '',
            details: '',
            uri: 'http://localhost:3000/projects/' + this.id
        }
    },
    mounted(){
        fetch(this.uri)
        .then(res => res.json())
        .then(data => {
            this.details = data.details
            this.title = data.title
        })
        .catch(err => console.log(err.message))
    },
    methods: {
        handleSubmit(){
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json'}, // دیتایی که برای اپدیت میفرستیم قالب جیسون باشه
                body: JSON.stringify({
                    title : this.title,
                    details : this.details
                }) // ارسال اطلاعات به صورت جیسون
            })
            .then(() => {
                this.$router.push('/')
            })
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>

</style>