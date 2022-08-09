<template>
    <div id="main-container">
        <h1>Monte seu burger</h1>
    </div>

    <form id="burger-form">
        <div class="input-container">
            <label for="nome">Nome do cliente</label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">

            <label for="nome">Nome do cliente</label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">

            <label for="pao">Escolha o pão: </label>
            <select name="pao" id="pao" v-model="pao">
                <option value="">Selecione seu pão</option>
                <option value="Integral">Integral</option>
            </select>

            <label for="pao">Escolha a carne do seu burger: </label>
            <select name="carne" id="carne" v-model="carne">
                <option value="">Selecione o tipo de carne</option>
                <option value="Maminha">Maminha</option>
            </select>

            <label for="opcionais">Selecione os opcionais: </label>
            <div class="checkbox-container">
                <input type="checkbox" name="opcionais" v-model="opcionais" value="salame">
                <span>Salame</span>
            </div>
     

        </div>
    </form>
</template>

<script>

export default{
    name: "BurgerForms"
}
</script>


<style scoped>
    #burgerform{
        display: block;
    }
</style>