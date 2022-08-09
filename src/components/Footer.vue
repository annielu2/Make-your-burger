<template>
    <footer id="footer">
        <p>Make your burger &copy; 2022</p>
    </footer>
</template>

<script>
export default {
    name: 'FooterComponent'
}
</script>

<style scoped>
    #footer{
        padding: 40px;
        background-color: #222;
        border-top: 4px solid #111;
        color:  rgb(133, 133, 133);
        display: flex;
        align-items: center;
        justify-content: center;
        bottom: 0;
        width: 100%;
        font-size: 0.9em;


    }
</style>