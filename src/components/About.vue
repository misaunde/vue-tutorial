<template>
    <div> 
        <h1 v-if="user_name">Hello {{ user_name }}, This is an about page</h1>
        <h1 v-else>This is an about page</h1>
        <p>BLA BLA aslkdfasd fasd fasdfasd fasdfasdf asdfkj;lksafd asdf asdf asdf asdfa dsf</p>    
    </div>  
</template>




<script>
export default {
    data() {
        return {
            user_name: this.$route.params.name
        }
    } 
}

</script>

<style scoped>

    /* body {
        background-color: #FFF !important;
    } */

</style>