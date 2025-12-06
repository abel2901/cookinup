<script lang="ts">
import Tag from "./Tag.vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: { Tag },

  props: {
    listaIngredientes: {
      type: Array as () => string[],
      required: true,
    },
  },
});
</script>

<template>
  <section>
    <span class="subtitulo-lg sua-lista-texto"> Sua lista: </span>

    <ul v-if="listaIngredientes.length" class="ingredientes-sua-lista">
      <li v-for="(ingrediente, index) in listaIngredientes" :key="index"></li>
    </ul>

    <p v-else class="paragrafo lista-vazia">
      <img
        src="../assets/imagens/icones/lista-vazia.svg"
        alt="Ícone de pesquisa"
      />
      Sua lista está vazia, selecione ingredientes para iniciar.
    </p>
  </section>
</template>

<style scoped>
.sua-lista-texto {
  color: var(--coral, #f0633c);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}
</style>
