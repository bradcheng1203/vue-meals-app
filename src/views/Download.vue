<template>
  <div class="max-w-[800px] mx-auto p-8 bg-slate-200">
    <h1 class="text-4xl font-bold mb-5 text-orange-500">{{ meal.strMeal }}</h1>    
    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-2">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">
            {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-2">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strMeasure${ind + 1}`]">
            {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>
    <div class="grid grid-cols-4 sm:grid-cols-4">
      <div class="mt-4">
        <YouTubeButton :href="meal.strYoutube" />
      </div>
      <div class="mt-4">
        <DownloadButton :href="meal.download" />
      </div>
      <div class="mt-4">
        <a :href="meal.download"
          target="_blank"
          class="ml-3 px-3 py-2 rounded border-2 border-transparent text-indigo-600 transition-colors" >
          Original Source
        </a>
      </div>
      <div class="mt-4">
        <a :href="meal.download">Remove City
        </a>
      </div>      
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';
import YouTubeButton from '../components/YouTubeButton.vue';
import DownloadButton from '../components/DownloadButton.vue';

const route = useRoute();
const meal = ref({})

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({ data }) => {      
      meal.value = data.meals[0] || {}
      meal.value.download = "https://www.heidisql.com/installers/HeidiSQL_12.8.0.6908_Setup.exe";
    })
})
</script>

