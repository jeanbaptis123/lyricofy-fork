<script setup lang="ts">
import { defineProps, ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();

interface IArtists {
  adamid: string;
}

type TArtists = IArtists[];

interface IProps {
  title: string;
  subtitle: string;
  images: {
    coverart: string;
  };
  artists: TArtists;
}

const { chart } = defineProps<{
  chart: IProps;
}>();
</script>

<template>
  <div
    class="flex flex-col w-[250px] p-4 bg-white/5 bg-opacity-80 backdrop-blur-sm animate-slideup rounded-lg cursor-pointer"
  >
    <div class="relative w-full h-56 group">
      <div
        class="absolute inset-0 justify-center items-center bg-black bg-opacity-50 group-hover:flex hidden"
      >
        <svg
          stroke="currentColor"
          fill="currentColor"
          stroke-width="0"
          viewBox="0 0 512 512"
          class="text-gray-300"
          height="35"
          width="35"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M256 8C119 8 8 119 8 256s111 248 248 248 248-111 248-248S393 8 256 8zm115.7 272l-176 101c-15.8 8.8-35.7-2.5-35.7-21V152c0-18.4 19.8-29.8 35.7-21l176 107c16.4 9.2 16.4 32.9 0 42z"
          ></path>
        </svg>
      </div>
      <img
        alt="song_img"
        :src="chart?.images?.coverart ? chart?.images?.coverart : undefined"
        class="w-full h-full rounded-lg"
      />
    </div>
    <div class="mt-4 flex flex-col">
      <p class="font-semibold text-lg text-white truncate">
        <RouterLink :to="`/songs/${chart.key}`">{{
          chart?.title ? chart?.title : null
        }}</RouterLink>
      </p>
      <p class="text-sm truncate text-gray-300 mt-1">
        <RouterLink
          :to="`/artists/${
            chart?.artists[0]?.adamid ? chart?.artists[0]?.adamid : null
          }`"
        >
          {{ chart?.subtitle ? chart?.subtitle : null }}
        </RouterLink>
      </p>
    </div>
  </div>
</template>
