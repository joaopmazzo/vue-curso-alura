<template>
  <div>
    <h1 class="centralizado">Alurapic</h1>
    <input
      type="search"
      class="filtro"
      @input="filtro = $event.target.value"
      placeholder="Filtre por parte do título1"
    />
    <ul class="lista_foto">
      <li
        class="lista_foto-itens"
        v-for="nomeGenerico of fotosComFiltro"
        :key="nomeGenerico"
      >
        <meu-painel :titulo="nomeGenerico.titulo">
          <imagem-responsiva
            :src="nomeGenerico.url"
            :alt="nomeGenerico.titulo"
          />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../components/shared/painel/Painel.vue";
import ImagemResponsiva from "../components/shared/imagem-responsiva/ImagemResponsiva.vue";

export default {
  components: {
    "meu-painel": Painel,
    "imagem-responsiva": ImagemResponsiva
  },
  data() {
    return {
      fotos: [],
      filtro: ""
    };
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        /* filtrar */
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
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
.centralizado {
  text-align: center;
}

.lista_foto {
  list-style: none;
}

.lista_foto .lista_foto-itens {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
