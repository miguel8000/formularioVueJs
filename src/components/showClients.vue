<template>
    <section :class="{'clientes': !isPremium, 'clientes-premium': isPremium,}">
        <div>
            <p>Nome: {{cliente.nome | processarNome}}</p>
            <p>Idade: {{cliente.idade}}</p>
            <!-- <p>idEspecial: {{ idEspecial }}</p> -->
            <button @click="mudarCor" :class="{'button': !isPremium, 'buttonSelect': isPremium}">Selecionar</button>
            <button @click="emitirEventoDelete" :class="{'button': !isPremium, 'buttonSelect': isPremium}">Exluir</button>
        </div>
    </section>
</template>

<script>
export default {
    data(){
        return {
            isPremium: false
        }
    },
    props:{
        cliente: Object,
    },
    methods:{
        mudarCor: function(){
            this.isPremium = !this.isPremium;
        },
        emitirEventoDelete: function(){
            this.$emit("meDelete", {idCliente: this.cliente.id});
        }
    },
    filters:{
        processarNome: function(value){
            return value.toUpperCase();
        }
    },
    computed:{
        idEspecial: function(){
            return (this.cliente.nome + this.cliente.idade + this.cliente.id).toUpperCase();
        }
    }
}
</script>

<style scoped>
    section{
        font-family: Arial, Helvetica, sans-serif;
        font-size: 12pt;
    }
    .clientes{
        background-color: white;
        padding: 10px;
        margin-bottom: 2%;
        padding: 10px;
        border-radius: 8px;
        transition: 0.5s ease-in-out;
        box-shadow:0 0 20px rgba(0,0,0,0.4);
    }

    .clientes-premium{
        background-color:#6495ED;
        color: white;
        padding: 10px;
        margin-bottom: 2%;
        padding: 10px;
        border-radius: 8px;  
        transition: 0.5s ease-in-out;              
    }
    .buttonSelect{
        background-color: white;
        border: 1px;
        border-radius: 5px;
        height: 30px;
        color: #6495ED;
        outline: none;
        transition: 0.5s ease-in-out;
    }
    .buttonSelect:hover{
        background-color: #6495ED;
        border: 1px solid white;
        color: white;
        transition:0.5s ease-in-out;
    }
</style>
