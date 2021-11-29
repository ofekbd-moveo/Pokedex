<template>
  <div>
    <!-- <button @click="printProps">click me</button> -->
    <card
      v-for="pokemon in pokemonsData"
      v-bind:key="pokemon.name"
      :id="pokemon.id"
      :name="pokemon.name"
      :imgSrc="pokemon.imgSrc"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Card from "./Card.vue";
import axios from "axios";
export interface Pokemon {
  id: number;
  name: string;
  imgSrc: string;
}

@Component({
  components: {
    Card,
  },
})
export default class CardList extends Vue {
  public pokemonsData: Array<Pokemon> = [];
  constructor() {
    super();
    this.getPokemons();
  }
  getPokemons(): void {
    console.log("sdfg");

    axios.get("https://pokeapi.co/api/v2/pokemon/").then((res: any) => {
      console.log(res);

      res.data.results.map((pokemon: { name: any; url: any }) => {
        const { name, url } = pokemon;
        axios.get(url).then((pokemonData) => {
          const imgSrc = (pokemonData as any).data.sprites.front_default;
          console.log(pokemonData);

          this.pokemonsData.push({ id: 1, name, imgSrc });
        });
      });
    });
  }

  //   mouted() {
  //     this.getPokemons();
  //   }
  printProps() {
    console.log(this.pokemonsData);
  }
}
</script>

function Component(arg0: { props: { pokemonsData: Pokemon[]; }; methods: { getPokemons(this: Vue): void;
printProps(this: Vue): void; }; }) { throw new Error("Function not implemented."); }
