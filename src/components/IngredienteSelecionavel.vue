<script lang="ts">
import Tag from "./Tag.vue";

export default {
  components: { Tag },
  props: {
    ingrediente: { type: String, required: true },
  },
  methods: {
    aoClicar() {
        this.selecionado = !this.selecionado

        if (this.selecionado) {
            this.$emit('adicionarIngrediente', this.ingrediente);
        }

        if (!this.selecionado) {
          this.$emit('removerIngrediente', this.ingrediente);
        }
    }
  },
  emits: ['adicionarIngrediente', 'removerIngrediente'],
  data() {
    return {
      selecionado: false,
    };
  },
};
</script>

<template>
  <button
    class="ingrediente"
    @click="aoClicar"
    :aria-pressed="selecionado"
  >
    <Tag :texto="ingrediente" :ativa="selecionado" />
  </button>
</template>

<style scoped>
.ingrediente {
    cursor: pointer;
}
</style>
