<template>
    <div class="container">
        
        <div id="main-container">
            <h1>Monte seu burger</h1>
        </div>
        <MessageComponent :msg="msg" v-show="msg"/>
        <form id="burger-form" @submit="createBurger" autocomplete="off">
            <div class="input-container">
                <label for="nome">Nome do cliente:</label>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome" class="styling">
            </div>

            <div class="input-container">
                <label for="pao">Escolha o pão: </label>
                <select name="pao" class="styling" id="pao" v-model="pao">
                    <option value="">Selecione seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
                </select>
            </div>
            
            <div class="input-container">
                <label for="carne">Escolha a carne do seu Burger:</label>
                <select name="carne" id="carne" v-model="carne" class="styling">
                    <option value="">Selecione o tipo de carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                </select>
      </div>            
             <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                    <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                    <span>{{ opcional.tipo }}</span>
                </div>
        </div>

            <div class="input-container">
                <input type="submit" class="submit-bnt" value="Crie seu hambúrguer!">
            </div>
        </form>
    </div>

</template>

<script>
  
import MessageComponent from './Message.vue';


export default{

    name: "BurgerForms",
    data(){
        return{
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            status: "Solicitado",
            msg: null

        }
    },

    methods: {
        async getIngredientes() {
            const req = await fetch('http://localhost:3000/ingredientes')
            const data = await req.json()
            this.paes = data.paes
            this.carnes = data.carnes
            this.opcionaisdata = data.opcionais
        },

        async createBurger(e) {
        e.preventDefault()
        const data = {
            nome: this.nome,
            carne: this.carne,
            pao: this.pao,
            opcionais: Array.from(this.opcionais),
            status: "Solicitado"
        }

            const dataJSON = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJSON
                
                });

            const res = await req.json();

            this.msg = "Pedido realizado com sucesso!";

            setTimeout(() => this.msg = "", 3000);

            this.nome = "";
            this.carne = "";
            this.opcionais = "";
            this.pao = "";
       }
    },

    mounted(){
        this.getIngredientes()
    },

    components: {
        MessageComponent
    }
}
</script>


<style scoped>


    
    #burger-form{
        max-width: 400px;
        margin: 0 auto;     
        background-color: rgb(241, 241, 241);
        padding: 40px;
        margin-bottom: 30px; 
        border-radius: 20px;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-size: 20px;
        font-weight: 600;
        margin-bottom: 15px;
        padding: 0 15px;
        color: #222;
        border-left: 2px solid #fcba30;
    }

    input, select{
        padding: 10px 10px;
        width: 300;
    }

    .styling{
        border-radius: 7px;
        background-color: white;
        border: 1px solid rgb(161, 161, 161)
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    
    }

    #opcionais-title{
        width: 100%;
    }

    .checkbox-container{
        display: flex;
        width: 50%;
        align-items: flex-start;
        margin-bottom: 20px;

    }
    
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left: 6px;
        width: auto;
        font-weight: 700;
    }

    .submit-bnt{
        background-color: #222;
        border: 1px solid #222;
        color: #fcba30;
        font-weight: 400;
        font-size: 18px;
        padding: 15px 20px;
        border-radius: 10px;
        cursor: pointer;
        transition: 0.5s;
    }

    .submit-bnt:hover{
        background-color: transparent;
        color: #222;
    }

</style>