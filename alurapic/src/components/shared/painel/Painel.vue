<template>
  <div class="painel">
    <h2 class="painel-titulo" @dblclick="visivel = !visivel">
      {{ titulo }}
    </h2>
    <transition name="painel-fade">
      <div class="painel-conteudo" v-show="visivel">
        <slot />
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["titulo"],
  data() {
    return {
      visivel: true
    };
  }
};
</script>

<style scoped>
* {
  box-shadow: 5px 5px 5px black;
}

/* estilo painel */
.painel {
  padding: 0 auto;
  border: solid 1px grey;
  display: inline-block;
  margin: 5px;
  box-shadow: 5px 5px 10px grey;
  width: 200px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}

.painel .painel-titulo {
  text-align: center;
  border: solid 2px;
  background: lightblue;
  margin: 0 0 15px 0;
  padding: 10px;
  text-transform: uppercase;
}

/* painel fade */
.painel-fade-enter,
.painel-fade-leave-active {
  opacity: 0;
}

.painel-fade-enter-active,
.painel-fade-leave-active {
  transition: opacity 0.4s;
}
</style>
