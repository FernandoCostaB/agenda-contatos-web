<template>
  <div>
    <h3>Lista de contatos</h3>
    <br/>
    <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#novoContato">
       Novo Contato
    </button>
    <br />
    <br />
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
              <button @click="edit(contato)" data-toggle="modal" data-target="#editarContato" class="btn btn-info">Editar</button>
              <button @click="remove(contato)" class="btn btn-danger">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

<!-- Modal Novo contato -->
<div class="modal fade"   id="novoContato" tabindex="-1" role="dialog" aria-labelledby="novoContato" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="novoContato">Novo Contato</h5>
      </div>
      <div class="modal-body">
        <Contato v-on:close="fecharModal" />
      </div>
      <div class="modal-footer">
        <button type="button" id="fechar" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>

<div v-if="show" class="modal fade"  id="editarContato" tabindex="-1" role="dialog" aria-labelledby="editarContato" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="editarContato">Editar Contato</h5>
      </div>
      <div class="modal-body">
        <Editar v-bind:contato="contato"  v-on:close="fecharModalEdicao" />
      </div>
      <div class="modal-footer">
        <button type="button" id="fecharEdicao" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
  </div>
</template>

<script>
import { Axios } from './common/http-common'
import Contato from './Contato.vue'
import Editar from './EditarContato.vue'

export default {
  components: {
    Contato: Contato,
    Editar: Editar
  },
  data () {
    return {
      contatos: [],
      visible: false,
      show: false,
      contato: ''
    }
  },
  mounted () {
    this.listarContatos()
  },
  methods: {
    edit (contatoToEdit) {
      this.contato = contatoToEdit
      this.show = true
    },
    fecharModalEdicao () {
      var botao = document.getElementById('fecharEdicao')
      botao.click()
      this.listarContatos()
    },
    fecharModal () {
      var botao = document.getElementById('fechar')
      botao.click()
      this.listarContatos()
    },
    listarContatos () {
      Axios.get('/contatos')
        .then(response => {
          this.contatos = response.data
          this.visible = true
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    remove (contato) {
      if (!confirm('Deseja relamente excluir este contato?')) return false
      Axios.delete('/contatos/' + contato.id)
        .then(response => {
          this.listarContatos()
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
