<script lang="ts">
export default {
  data() {
    return {
      receitas: [] as any[],
      error: null as Error | null,
    };
  },

  async mounted() {
    try {
      const res = await fetch(
        "https://gist.githubusercontent.com/antonio-evaldo/002ad55e1cf01ef3fc6ee4feb9152964/raw/bf463b47860043da3b3604ca60cffc3ad1ba9865/receitas.json"
      );

      if (!res.ok) {
        throw new Error(`Erro ao buscar JSON: ${res.status}`);
      }

      this.receitas = await res.json();
    } catch (err) {
      this.error = err as Error;
    }
  },
};
</script>

<template>
  <section class="selecionar-receita">
    <h1 class="cabecalho titulo-receita">Receitas</h1>
    <p class="paragrafo-lg dica">
      Veja as opções de receitas que encontramos com os ingredientes que você
      tem por aí!
    </p>
    <ul class="categoria__receitas">
      <li class="card__receita" v-for="(receita, index) in receitas" :key="index">
        <img class="img_receitas":src="`imagens/receitas/${receita.imagem}`" />
        <p class="nome__receita">{{ receita.nome }}</p>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.selecionar-receita {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-receita {
  color: var(--verde-medio, #3d6d4a);
  display: block;
  margin-bottom: 1.5rem;
  font-weight: 400;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

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
