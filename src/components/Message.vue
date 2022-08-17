<template>
    <div class="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>
export default{
    name: "MessageComponent",
    props: {
        msg: String
    }

}
</script>

<style scoped>
    .message-container{
        max-width: 400px;
        margin: 30px auto;
        color: rgb(91, 132, 182);
        font-size: 16px;
        background-color: rgb(228, 238, 252);
        padding: 10px;
        border: 1px solid rgb(163, 190, 223);
        border-radius: 5px;
    }

</style>
