<template>
  <div class="project" :class="{complete: project.complete}">
    <div class="actions">
        <h3 @click="showActions">{{project.title}}</h3>
        <div class="icons">
            
            <router-link :to="{name: 'EditProject', params: {id: project.id}}">
                <i class="fa-solid fa-pen-to-square"></i>
            </router-link>

            <i @click="changeComplete" class="fa-sharp fa-solid fa-square-check"></i>
            <i @click="deleteTrash" class="fa-sharp fa-solid fa-trash"></i>
        </div>
    </div>
    <div class="details">
        <p v-if="showDetails">{{project.details}}</p>
    </div>
  </div>
</template>

<script>
export default {
    props: ['project'],
    data(){
        return{
            showDetails : false,
            uri: 'http://localhost:3000/projects/' + this.project.id
        }
    },
    methods : {
        showActions(){
            this.showDetails = !this.showDetails
        },
        deleteTrash(){
             fetch(this.uri, {method: 'DELETE'})
            .then(() => this.$emit('delete',this.project.id))
            .catch(err => console.log(err.message))
        },
        changeComplete(){
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json'}, // دیتایی که برای اپدیت میفرستیم قالب جیسون باشه
                body: JSON.stringify({complete: !this.project.complete}) // ارسال اطلاعات به صورت جیسون
                })
                .then(() => this.$emit('complete',this.project.id))
                .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>
.project{
    background-color: #fff;
    margin: 20px auto;
    padding: 10px 10px;
    border-left: 4px solid #e90074;
    border-radius: 5px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
}
h3{
    cursor: pointer;
}
.actions{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.fa-solid{
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}
.fa-solid:hover{
    color: #777;
}
.project.complete{
    border-left: 4px solid #00ce89;
}

</style>