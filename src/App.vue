<script setup>
import { ref } from 'vue';

const produtos = ref([
    {
        id: 1,
        nome: 'Camiseta',
        preco: 49.90,
        quantidade: 1
    },
    {
        id: 2,
        nome: 'Calça',
        preco: 99.90,
        quantidade: 1
    },
    {
        id: 3,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 1
    },
    {
        id: 4,
        nome: 'Sapato',
        preco: 199.90,
        quantidade: 1
    },
    {
        id: 5,
        nome: 'Boné',
        preco: 29.90,
        quantidade: 1
    },
    {
        id: 6,
        nome: 'Óculos',
        preco: 99.90,
        quantidade: 1
    },
    {
        id: 7,
        nome: 'Relógio',
        preco: 299.90,
        quantidade: 1
    },
    {
        id: 8,
        nome: 'Bermuda',
        preco: 79.90,
        quantidade: 1
    },
    {
        id: 9,
        nome: 'Cueca',
        preco: 19.90,
        quantidade: 1
    },
    {
        id: 10,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 1
    }
])
let carrinho = ref([])
function addcarrinho(item){
  carrinho.value.push({
    codigo: item.id,
    nome: item.nome,
    preco: item.preco,
    quantidade: item.quantidade,
    valortotal: item.preco * item.quantidade
  })
}
function addquant(index){
    produtos.value[index].quantidade++
    // somaitem.value = item.preco * item.quantidade
  }

function limpacarrinho(){
  carrinho.value = []
}
function remover(index) {
    carrinho.value.splice(index, 1)
  }

const  avf = (value) => "R$ " + value.toFixed(2).replace('.',',')

</script>

<template>
  <ul>
    <li v-for="(item, index) in produtos" :key="index">Item: {{ item.nome }} Valor: {{ avf(item.preco) }} Quantidade: {{ item.quantidade }}
      <button @click="addcarrinho(item)">adicionar ao carrinho</button>
      <button @click="addquant(item.id-1)">+</button>
    </li>
  </ul>
  <div class="carrinho">
    <p>carrinho</p>
<ul>
  <li v-for="(item, index) in carrinho" :key="index">{{ item.nome }} {{ avf(item.preco) }} {{ item.quantidade }} valor total {{ avf(item.valortotal) }}
  <button @click="remover(index)">remover</button></li>
</ul>
  <button @click="limpacarrinho()">limpa carrinho</button>
  </div>
</template>

<style scoped>

</style>
