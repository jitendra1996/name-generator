<template>
  <div class="m-auto w-1/2 text-center">
    <h1
      class="text-5xl mb-5 uppercase font-extralight tracking-widest text-purple-400"
    >
      Baby Name Generator
    </h1>
    <p class="text-2xl mb-3 text-purple-500">
      Choose your optiond and click the "Find Names" Button below
    </p>
    <div class="bg-pink-300 text-white p-5 rounded-md">
      <div class="mb-4">
        <h4 class="text-xl mb-5">1) Choose a gender</h4>
        <div class="">
          <button
            class="px-10 py-1 border rounded-l-full text-xl font-sans"
            :class="options.gender === Gender.BOY && 'bg-pink-400'"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="px-10 py-1 border text-xl font-sans"
            :class="options.gender === Gender.UNISEX && 'bg-pink-400'"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            class="px-10 py-1 border rounded-r-full text-xl font-sans"
            :class="options.gender === Gender.GIRL && 'bg-pink-400'"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="mb-4">
        <h4 class="text-xl mb-5">2) Choose the name's popularity</h4>
        <div class="">
          <button
            class="px-10 py-1 border rounded-l-full text-xl font-sans"
            :class="options.popularity === Popularity.TRENDY && 'bg-pink-400'"
            @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            class="px-10 py-1 border rounded-r-full text-xl font-sans"
            :class="options.popularity === Popularity.UNIQUE && 'bg-pink-400'"
            @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="mb-8">
        <h4 class="text-xl mb-5">3) Choose name's length</h4>
        <div class="">
          <button
            class="px-10 py-1 border rounded-l-full text-xl font-sans"
            :class="options.length === Length.LONG && 'bg-pink-400'"
            @click="options.length = Length.LONG"
          >
            Long
          </button>
          <button
            class="px-10 py-1 border text-xl font-sans"
            :class="options.length === Length.SHORT && 'bg-pink-400'"
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
          <button
            class="px-10 py-1 border rounded-r-full text-xl font-sans"
            :class="options.length === Length.ALL && 'bg-pink-400'"
            @click="options.length = Length.ALL"
          >
            All
          </button>
        </div>
      </div>
      <hr class="mb-8 w-9/12 m-auto" />
      <button
        class="bg-pink-400 px-10 py-2 rounded-l-full rounded-r-full text-center text-xl font-sans hover:bg-pink-500"
        @click="computeSomeNames"
      >
        Find Name
      </button>
    </div>
    <div class="m-8 flex flex-wrap">
      <div
        v-for="(selectedName, index) in selectedNames"
        :key="index"
        class="m-2 w-1/4 bg-purple-400 text-white px-6 py-3 rounded-l-full rounded-r-full"
      >
        {{ selectedName }}
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { Gender, Popularity, Length, names } from "@/data";

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const obj: OptionsState = {
  gender: Gender.GIRL,
  popularity: Popularity.TRENDY,
  length: Length.SHORT,
};

const options = reactive(obj);

const selectedNames = ref<string[]>([]);

const computeSomeNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });

  selectedNames.value = filteredNames.map((name) => name.name);
};
</script>
