<script lang="ts">
import type { PropType } from "vue";

type Receita = {
  nome: string;
  imagem: string;
  categoria: string;
};

export default {
  props: {
    receitas: {
      type: Array as PropType<Receita[]>,
      required: true,
    },
  },
};
</script>

<template>
  <section>
    <ul class="categoria__receitas">
      <li
        class="card__receita"
        v-for="(receita, index) in receitas"
        :key="index"
      >
        <img class="img_receitas" :src="`imagens/receitas/${receita.imagem}`" />
        <p class="nome__receita">{{ receita.nome }}</p>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.categoria__receitas {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.5rem;
  list-style: none;
  padding: 0;
}

.card__receita {
  padding: 1rem;
  text-align: center;
}

.img_receitas {
  width: 100%;
  border-top-left-radius: 16px;
  border-top-right-radius: 16px;
  object-fit: cover;
}

.nome__receita {
  font-style: normal;
  font-weight: 700;
  align-items: center;
  color: #444444;
  text-align: center;
  margin-top: 32px;
}
</style>
