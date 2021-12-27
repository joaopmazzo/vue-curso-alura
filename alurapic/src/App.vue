<template>
  <div>
    <h1 v-text="titulo"></h1>
    <ul>
      <li v-for="nomeGenerico of fotos" :key="nomeGenerico">
        <img :src="nomeGenerico.url" :alt="nomeGenerico.titulo">
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: 'AluraPic',
      fotos: []
    }
  },
  created() {
    this.$http.get('http://localhost:3000/v1/fotos') // realiza a consulta no endereço da API
      .then(res => res.json())  // pega os dados do retorno e transforma em um json (que tambem é uma promise)
      .then(fotos => this.fotos = fotos, err => console.log(err));  // pega esse json e passa para o nosso array de fotos e, caso não consiga retornar nada dessa "promessa", mostra o erro no console
  }
}
</script>

<style>

</style>