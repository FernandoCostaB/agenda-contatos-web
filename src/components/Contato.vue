<template>
  <div>
<form>
  <div class="form-group row">
    <label  class="col-sm-2 col-form-label" for="Nome">Nome</label>
     <div class="col-sm-10">
    <input type="text" class="form-control" v-model="nome" id="Nome" placeholder="Digite o nome">
    </div>
  </div>
  <div class="form-group row">
    <label for="inputEmail3" class="col-sm-2 col-form-label">Email</label>
    <div class="col-sm-10">
      <input type="email" class="form-control" v-model="email" id="inputEmail3" placeholder="Email">
    </div>
  </div>
   <div class="form-group row">
    <label for="Telefone" class="col-sm-2 col-form-label">Telefone</label>
    <div class="col-sm-10">
    <input type="text" class="form-control" v-model="telefone" id="Telefone" placeholder="Digite o telefone">
    </div>
  </div>
  <fieldset class="form-group">
    <div class="row">
      <legend class="col-form-label col-sm-2 pt-0">Sexo</legend>
      <div class="col-sm-10">
        <div class="form-check">
          <input class="form-check-input" v-model="sexo" type="radio" name="gridRadios" id="gridRadios1" value="feminino" >
          <label class="form-check-label" for="gridRadios1">
            Feminino
          </label>
        </div>
        <div class="form-check">
          <input class="form-check-input" v-model="sexo" type="radio" name="gridRadios" id="gridRadios2" value="masculino">
          <label class="form-check-label" for="gridRadios2">
            Masculino
          </label>
        </div>
      </div>
    </div>
  </fieldset>
   <div class="col-auto">
      <button type="button" @click="salvarContato" class="btn btn-primary mb-2">Salvar</button>
    </div>
</form>
  </div>
</template>

<script>
import { Axios } from './common/http-common'
export default {
  data () {
    return {
      nome: '',
      sexo: '',
      telefone: '',
      email: ''
    }
  },
  methods: {
    salvarContato () {
      const param = {
        nome: this.nome,
        sexo: this.sexo,
        telefone: this.telefone,
        email: this.email
      }
      Axios.post('/contatos', param)
        .then(response => {
          console.log(response)
          this.$emit('close')
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
