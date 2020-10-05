<template>
  <div>
    <h3>Lista de contatos</h3>
    <br />
    <div v-if="visible">
       <div v-for="contato in contatos" :key="contato.id">
       <p>{{ contato.nome }}</p>
    </div>
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
  mounted () { this.listarContatos() },
  methods: {
    listarContatos () {
      Axios.get('/contatos')
        .then((response) => {
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
