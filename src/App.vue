<template>
  <div class="conteiner" id="app">
    <div>
      <h1>Projeto Vue de Cadastro de Nome e Idade</h1>
    </div>
    <div class="error" v-show="error">
      O nome ou idade Invalido
    </div>
    <div class="inputs">
      <input type="text" placeholder="Name" v-model="nomeField">
      <input type="text" placeholder="Idade" v-model="idadeField">
      <button class="cadastrar" @click="cadastrar">Cadastrar</button>
    </div>
    <div v-for="clientes in orderClients" :key="clientes.id">
      <showClients class="showClients" :cliente="clientes" @meDelete="deletar"/>
    </div>  
  </div>
</template>

<script>
import _ from 'lodash';
import showClients from './components/showClients.vue'

export default {
  name: 'App',
  data(){
     return {
      
       nomeField: "",
       idadeField: "",
       error: false,
       clientes:[
        {
          id: 4354321,
          nome: "miguel",
          idade: "26"
        }
       ]
     }
     
    },
  
  components: {
    showClients
  },
  methods:{

    cadastrar: function(){
      if(this.nomeField == "" || this.nomeField == " " || this.nomeField.length == 0){
        this.error = true;
      }else{
        this.clientes.push({nome: this.nomeField, idade:this.idadeField, id: Date.now()});
        this.nomeField = "";
        this.idadeField = 0;
        this.error = false;
      }  
    },

    deletar: function($event){
      let id = $event.idCliente;
      let novoArray = this.clientes.filter(clientes => clientes.id != id);
      this.clientes = novoArray;
    }
  },
  computed: {
    orderClients: function(){
      return _.orderBy(this.clientes,['nome'],['asc']);
    }
  }
}
</script>

<style>
  body{
    font-family: Arial, Helvetica, sans-serif;
    background-color: lightgray;
    transition: all 0.5s ease-in-out;
    display: flex;
    justify-content: center;
  
  }
  h1{
    text-align: center;
    margin-bottom: 2%;
  }
  .inputs{
    display: flex;
    flex-wrap: wrap;
  }
  .error{
    color: red;
    padding-left: 10px;
    padding-bottom: 10px;
  }
  input{
    height: 30px;
    border: 0px;
    border-radius: 5px;
    padding: 3px;
    margin-bottom: 2%;
    margin-left: 10px;
    outline: none;
  }
  input:hover{
    box-shadow:0 0 20px rgba(0,0,0,0.4);
  }
  input:focus{
    box-shadow:0 0 20px rgba(0,0,0,0.4);
  }
  button{
    background-color: #6495ED;
    border: 1px;
    border-radius: 5px;
    height: 36px;
    color: white;
    outline: none;
    margin-left: 10px;
    transition: 0.5s ease-in-out;
  }
  button:hover{
    background-color: white;
    border: 1px solid #6495ED;
    color: #6495ED;
    transition:0.5s ease-in-out;
  }  
  .showClients{
    animation-name: card;
    animation-duration: 1s;
  }
  @keyframes card{
    from{
      transform: translateX(-300px);
      opacity: 0;
    }
    to{
      transform: translateX(0);
      opacity: 1;
    }
  }
  @media screen and (max-width: 480px) {
  input {
    width: 100%;
    margin-left: 0;
  }
  .cadastrar{
    width: 100%;
    margin-bottom: 2%;
    margin-left: 0;
  }
}
</style>
