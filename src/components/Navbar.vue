<template>
  <div class="main-nav">
    <router-link :to="{name : 'Home'}">Projects</router-link>
    <router-link :to="{name : 'AddProject'}">Add a new project</router-link>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.main-nav{
    text-align: center;
    margin: 40px auto;
    display: flex;
    justify-content: space-between;
    width: 300px;
}
.main-nav a{
    text-decoration: none;
    color: #999;
    font-size: 18px;
}
a.router-link-active{
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
}

</style>