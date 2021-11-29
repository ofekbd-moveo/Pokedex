<template>
  <div>
    <div class="pokemon-id">{{ id }}</div>
    <img :src="`${imgSrc}`" />
    <div>{{ name }}</div>
    <button @click="printProps"></button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  props: {
    id: Number,
    name: String,
    imgSrc: String,
  },
  methods: {
    printProps() {
      console.log(this.$props);
    },
  },
})
export default class Card extends Vue {}
</script>
