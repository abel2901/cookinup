<script lang="ts">
import ListaCategoriaReceita from './ListaCategoriaReceita.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';

export default {
  data() {
    return {
      receitas: [] as any[],
      error: null as Error | null,
      pagina: 'ConteudoPrincipal'
    };
  },
  emits: ['editarReceitas'],
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
  components: { ListaCategoriaReceita, BotaoPrincipal },
};
</script>

<template>
  <section class="selecionar-receita">
    <h1 class="cabecalho titulo-receita">Receitas</h1>
    <p class="paragrafo-lg dica">
      Veja as opções de receitas que encontramos com os ingredientes que você
      tem por aí!
    </p>
    <ListaCategoriaReceita :receitas="receitas" />
    <BotaoPrincipal texto="Editar Lista" @click="$emit('editarReceitas')"/>
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
  margin-bottom: 3.5rem;
  text-align: center;
}

</style>
