<script setup>
import { ref } from 'vue'

const produtos = ref([
  {
    id: 1,
    nome: 'Camiseta',
    preco: 49.9,
    quantidade: 1,
  },
  {
    id: 2,
    nome: 'Calça',
    preco: 99.9,
    quantidade: 1,
  },
  {
    id: 3,
    nome: 'Meia',
    preco: 9.9,
    quantidade: 1,
  },
  {
    id: 4,
    nome: 'Sapato',
    preco: 199.9,
    quantidade: 1,
  },
  {
    id: 5,
    nome: 'Boné',
    preco: 29.9,
    quantidade: 1,
  },
  {
    id: 6,
    nome: 'Óculos',
    preco: 99.9,
    quantidade: 1,
  },
  {
    id: 7,
    nome: 'Relógio',
    preco: 299.9,
    quantidade: 1,
  },
  {
    id: 8,
    nome: 'Bermuda',
    preco: 79.9,
    quantidade: 1,
  },
  {
    id: 9,
    nome: 'Cueca',
    preco: 19.9,
    quantidade: 1,
  }
])
const avf = (value) => 'R$ ' + value.toFixed(2).replace('.', ',')
let enviar = ref(false)
let carrinho = ref([])
let valorcarrinho = ref(0)

function addcarrinho(item) {
  const index = carrinho.value.findIndex((x) => x.codigo === item.id)
  if (index > -1) {
    alert('item já está no carrinho')
  } else {
    carrinho.value.push({
      codigo: item.id,
      nome: item.nome,
      preco: item.preco,
      quantidade: item.quantidade,
      valortotal: item.preco * item.quantidade
    })
    calculacarrinho()
  }
}

function calculacarrinho() {
  valorcarrinho.value = 0
  for (let index = 0; index < carrinho.value.length; index++) {
    valorcarrinho.value = valorcarrinho.value + carrinho.value[index].valortotal
  }
}

function addquant(index) {
  produtos.value[index].quantidade++
}

function removerquant(index) {
  if (produtos.value[index].quantidade > 1) {
    produtos.value[index].quantidade--
  }
  // somaitem.value = item.preco * item.quantidade
}

function limpacarrinho() {
  carrinho.value = []
  valorcarrinho.value = 0
}
function remover(index) {
  carrinho.value.splice(index, 1)
  calculacarrinho()
}
function vercarrinho() {
  if (carrinho.value < [0]) {
    alert('carrinho vazio')
  } else {
    enviar.value = !enviar.value
  }
}

</script>

<template>
  <h1>MIAUMIAUMIAU</h1>
  <div class="dropdown">
    <button class="btn btn-dark dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown"
      aria-haspopup="true" aria-expanded="false" @click="vercarrinho">Ver carrinho</button>
    <div class="dropdown-menu carrinho" v-if="enviar">
      <div class="items-carrinho">
        <div v-for="(item, index) in carrinho" :key="index" class="item-carrinho">
          <p>Produto: {{ item.nome }}</p>
          <p>Preço:{{ avf(item.preco) }}</p>
          <p>Quantidade: {{ item.quantidade }}</p>
          <button class="btn btn-dark btn-sm" @click="remover(index)">remover</button>
        </div>
      </div>
      <div class="resumo-carrinho">
        <p class="dropdown-item-text">Valor total: {{ avf(valorcarrinho) }}</p>
        <button class="btn btn-dark btn-sm dropdown-item" @click="limpacarrinho()">limpa carrinho</button>
        <button class="btn btn-dark btn-sm dropdown-item" @click="enviar = !enviar">Fechar Carrinho</button>
      </div>
    </div>
  </div>
  <div class="produtos">
    <ul>
      <li v-for="(item, index) in produtos" :key="index">
        <p>Item: {{ item.nome }}</p>
        <p>Valor: {{ avf(item.preco) }}</p>
        <p>Quantidade: {{ item.quantidade }}</p>
        <p>
          <button class="btn btn-dark btn-sm" @click="addcarrinho(item)">adicionar ao carrinho</button>
          <button class="btn btn-dark btn-sm" @click="addquant(item.id - 1)">+</button>
          <button class="btn btn-dark btn-sm" @click="removerquant(index)">-</button>
        </p>
      </li>
    </ul>
  </div>
</template>

<style scoped>
ul {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
}

li {
  justify-content: center;
  align-items: center;
  text-align: center;
  list-style: none;
}

button {
  margin: 3px;
}

p {
  font-size: large;
}

.produtos {
  width: 900px;
  display: flex;
  align-items: center;
  text-align: center;
  margin: 50px auto;
  padding: 15px;
}

.carrinho {
  position: absolute;
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  left: 0;
  right: 0;
  width: 50%;
  align-items: center;
}

.items-carrinho {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  text-align: center;
  justify-content: center;
  padding: 5px;
  margin-left: auto;
  margin-right: auto;
}

.item-carrinho{
  margin: 10px;
}


.dropdown {
  background-color: pink;
}
</style>
