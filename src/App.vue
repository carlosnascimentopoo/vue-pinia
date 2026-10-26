<template>
<section class="container">
<div>
  <form @submit.prevent="adicionar">
    <input type="text" v-model="nome" placeholder="Nome completo"/>
    <input type="email" v-model="email" placeholder="E-mail"/>
    <button type="submit">adicionar</button>
  </form>
</div>
<ul>
  <li v-for="dado in dados" :key="dado.id">
  <span><strong>nome:</strong>{{dado.nome}}</span>
  <p>{{dado.email}}</p>
  <button @click="remover(dado.id)">Excluir</button>
  </li>
</ul>
</section>
</template>

<script setup>
import {ref} from 'vue';
const nome = ref('');
const email = ref('');

 const dados = ref([
 {
  id:1,
  nome:"carlos",
  email:"carlos@gmail.com"
 },
 {
 id:2,
  nome:"jose",
  email:"jose@gmail.com"
 },
 {
 id:3,
  nome:"deliany",
  email:"deliany@gmail.com"
  }
 ])

 function adicionar(){

  if(!nome.value.trim() || !email.value.trim()){
    alert("Campos obrigatório!");
    return;
  }

  const jaCadastrado = dados.value.find(item=>item.email === email.value)

  if(jaCadastrado){
    alert("Email já cadastrado, TENTE OUTRO E-MAIL")
    return;
  }

  dados.value.push({
    id:Date.now(),
    nome:nome.value,
    email:email.value
  })
  alert("Adicionado com sucesso")
  nome.value = '';
  email.value = '';
 }


function remover(id){
if(confirm("Deseja excluir contato")){
  dados.value = dados.value.filter(item=>item.id !== id);
}
 }
</script>


<style>

.container{
display:flex;
    flex-direction:column;
    gap:10px;
    margin:0 auto;
    max-width:400px;
}
  form{
    display:flex;
    flex-direction:column;
    gap:10px;
    margin:0 auto;
    max-width:400px;
  }

  form input{
    padding:13px;
  }

  ul{
    padding:0;
    margin:0;
  }

  li{
    list-style:none;
    padding:1rem;
    border:1px solid #ccc;
    margin: .4rem 0;
  }
</style>