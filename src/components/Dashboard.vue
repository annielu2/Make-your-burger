<template>
    <div id="main-container">
        <h1>Gerenciar Pedidos</h1>
    </div>

    <MessageComponent :msg="msg" v-show="msg"/>
    
    <div id="burger-table">
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente: </div>
                <div>Pão: </div>
                <div>Carne: </div>
                <div>Opcionais: </div>
                <div>Ações</div>
            </div>
            <div id="burger-table-rows">
                <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
                    <div class="order-number">{{burger.id}}</div>
                    <div>{{burger.nome}}</div>
                    <div>{{burger.pao}}</div>
                    <div>{{burger.carne}}</div>
                    <div>
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">
                                {{opcional}}
                            </li>
                        </ul>
                    </div>
                    <div>
                        <select name="status" class="status" @change="updateBurger($event, burger.id)">
                            <option v-for="stts in status" :key="stts.id" :value=stts.tipo :selected="burger.status == stts.tipo">
                                {{stts.tipo}}
                            </option>
                        </select>
                        <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
 
 import MessageComponent from './Message.vue'
 
 export default {
    name: "DashboardComponent",
    data() {
      return {
        burgers: null,
        burger_id: null,
        status: [],
        msg: null
      }
    },

    components: {
        MessageComponent
    },

    methods: {
      async getPedidos() {
        const req = await fetch('http://localhost:3000/burgers')
        
        const data = await req.json()

        this.burgers = data
        
        this.getStatus()

      },

      async getStatus(){
        const req = await fetch('http://localhost:3000/status')
        
        const data = await req.json()

        this.status = data
        
      },

      async deleteBurger(id){
         const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "DELETE"
         });

         const res = await req.json();

         this.getPedidos();

         this.msg = "Pedido removido com sucesso!";

         setTimeout(() => this.msg = "", 3000);
      },

      async updateBurger(event, id){
         const option = event.target.value;

         const dataJson = JSON.stringify({status : option});

         const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "PATCH",
            headers: {"Content-Type" : "application/json"},
            body: dataJson
         });

         const res = await req.json();

         this.msg = "Pedido atualizado com sucesso!";

         setTimeout(() => this.msg = "", 3000);

      }


    },
    mounted () {
    this.getPedidos()
    }
  }
</script>

<style scoped>
    #burger-table{
        max-width: 1200px;
        margin: 0 auto;
    }

    #burger-table-heading, #burger-table-rows,
    .burger-table-row{
        display: flex;
        flex-wrap: wrap;
    }

    #burger-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 2px solid  #222;
        margin-bottom: 5px;

    }

    #burger-table-heading div, 
    .burger-table-row div{
        width: 19%;
    }

    .burger-table-row{
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #bbb;
    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number{
        width: 5%;
    }

    select{
        padding: 6px 12px;
        border-radius: 5px;
        background-color: white;
        border: 1px solid rgb(161, 161, 161);
        margin-right: 12px;
    }

    .delete-btn{
        background-color: #222;
        border: 1px solid #222;
        color: #fcba30;
        font-weight: 400;
        padding: 6px 12px;
        border-radius: 7px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s;
    }

    .delete-btn:hover{
        background-color: transparent;
        color: #222;
    }
</style>