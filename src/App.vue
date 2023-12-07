<script setup>
import { reactive } from 'vue';

const nome = 'Lukas'
const meuObj = {
  sobrenome: 'Tavares',
  filmeFavorito: 'Supernatural'
}

function dizOla(nome) {
  return `${nome} disse oi.`
}

const deanImg = 'https://upload.wikimedia.org/wikipedia/pt/b/b0/DeanWinchester.png'
const samImg = 'https://i.pinimg.com/736x/ec/b6/48/ecb64872fb1c6fdc2ff0ca47e0fb90d2.jpg'

const likeDean = false
const likeSam = false

const botaoDesabilitado = true

const estaAutorizado = true

//let contador = 0
const estado = reactive( {
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['Lucas', 'Rafael', 'Yago', 'Rafaela'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador++
}

function decrementar() {
  estado.contador--
}

function alteraEmail(evento) {
  estado.email = evento.target.value
}

function mostraSaldoFuturo() {
  const { saldo, transferindo} = estado
  return saldo - transferindo
}

function validaValorTransferencia() {
  const { saldo, transferindo} = estado
  return saldo >= transferindo
}

function cadastrarNome() {
  if (estado.nomeAInserir.length >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite o nome completo")
  }
}
</script>

<template>
  <h1>{{ nome }} {{ meuObj.sobrenome }}</h1>
  <h2>{{ dizOla('Rafaela') }}</h2>

  <img v-if="likeDean" :src="deanImg" alt="">
  <img v-else-if="likeSam" :src="samImg" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem-vindo ADM</h1>
  <h1 v-else>Faça o login</h1>

  <button :disabled="botaoDesabilitado">Enviar</button>

  <br>
  <hr>

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br>
  <hr>

  {{ estado.email }}
  <input type="text" @keyup="alteraEmail">

  <br>
  <hr>

  Saldo: {{ estado.saldo }}
  <br>
  Transferindo: {{ estado.transferindo }}
  <br>
  Saldo depois da transferência: {{ mostraSaldoFuturo() }}
  <br>
  <input class="campo" :class="{ invalido: !validaValorTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="validaValorTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastrarNome" type="button">Cadastrar nome</button>

  <h3 v-for="nome in estado.nomes"> {{ nome }}</h3>
</template>

<style scoped>
h1, h2 {
  font-family: sans-serif;
}

img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
}

.campo {
  border: 2px solid #000;
}
</style>
