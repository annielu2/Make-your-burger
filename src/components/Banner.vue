<template>
    <div id="main-container">
         <h1>Make your burger</h1>
    </div>
</template>


<script>

export default{
    name: "BannerComponent"
}
</script>

<style scoped>
    #main-container{
        background-image: url('../assets/burger.jpg');
        background-position: 0 -250px;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-container h1{
        color:rgb(223, 223, 223);
        background-color: rgba(0, 0, 0, 0.65);
        padding: 30px;
        border-radius: 10px;
    }

</style>