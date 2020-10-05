<template>
  <div>
    <h3>Lista de contatos</h3>
    <br />
    <div v-if="visible">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Nome</th>
            <th scope="col">Sexo</th>
            <th scope="col">Telefone</th>
            <th scope="col">Email</th>
            <th scope="col">Ação</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contato in contatos" :key="contato.id">
            <th scope="row">{{ contato.id }}</th>
            <td>{{ contato.nome }}</td>
            <td>{{ contato.sexo }}</td>
            <td>{{ contato.telefone }}</td>
            <td>{{ contato.email }}</td>
            <td>
              <button @click="edit(item)" class="btn btn-info">Editar</button>
              <button @click="remove(item)" class="btn btn-danger">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { Axios } from './common/http-common'

export default {
  data () {
    return {
      contatos: [],
      visible: false
    }
  },
  mounted () {
    this.listarContatos()
  },
  methods: {
    listarContatos () {
      Axios.get('/contatos')
        .then(response => {
          this.contatos = response.data
          this.visible = true
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  }
}
</script>

<style>
</style>
