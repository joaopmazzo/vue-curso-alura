<template>
  <div class="corpo">
    <h1 class="centralizado" v-text="titulo"></h1>
    <ul class="lista_foto">
      <li
        class="lista_foto-itens"
        v-for="nomeGenerico of fotos"
        :key="nomeGenerico"
      >
        <meu-painel :titulo="nomeGenerico.titulo">
          <img
            class="imagem-responsiva"
            :src="nomeGenerico.url"
            :alt="nomeGenerico.titulo"
          />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "./components/shared/painel/Painel.vue";
export default {
  components: {
    "meu-painel": Painel
  },
  data() {
    return {
      titulo: "AluraPic",
      fotos: []
    };
  },
  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos") // realiza a consulta no endereço da API
      .then(res => res.json()) // pega os dados do retorno e transforma em um json (que tambem é uma promise)
      .then(
        fotos => (this.fotos = fotos),
        err => console.log(err)
      ); // pega esse json e passa para o nosso array de fotos e, caso não consiga retornar nada dessa "promessa", mostra o erro no console
  }
};
</script>

<style>
.corpo {
  font-family: Arial, Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}

.centralizado {
  text-align: center;
}

.lista_foto {
  list-style: none;
}

.lista_foto .lista_foto-itens {
  display: inline-block;
}

.imagem-responsiva {
  width: 100%;
}
</style>
