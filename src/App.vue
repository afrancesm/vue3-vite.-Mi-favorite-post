<script setup>

import { ref, computed, onMounted } from 'vue';

import BlogPost from './components/BlogPost.vue';
import PaginatePosts from './components/PaginatePosts.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);
const favorito = ref('');
const postPorPagina = 9;
const posInicio = ref(0);
const posFin = ref(postPorPagina);
const loading = ref(true);

const cambiarFavoritoMethod = (title) => {
  favorito.value = title;
}


onMounted(async() => {
  loading.value = true;
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  }catch(error){

  }finally{
    setTimeout(() => {
      loading.value = false
    }, 2000)
  }
})

/*
fetch('https://jsonplaceholder.typicode.com/posts')
  .then((res) => res.json())
  .then((data) => (posts.value = data))
  .catch((e) => console.log(e))
  .finally(() => {
    setTimeout(() => {
      loading.value = false
    }, 2000)
  });
*/
const next = () => {
  posInicio.value += postPorPagina;
  posFin.value += postPorPagina;
}

const prev = () => {
  posInicio.value -= postPorPagina;
  posFin.value -= postPorPagina;
}

const maxLength = computed(() => posts.value.length);


</script>

<template>

<LoadingSpinner v-if="loading"></LoadingSpinner>

  <div class="container" v-else>
    <h1>App</h1>

    <h2>Mi Post Favorito:</h2>
    <p>{{ favorito }}</p>

    <section>
      <PaginatePosts
      @next="next"
      @prev="prev"
      :inicio="posInicio"
      :fin="posFin"
      :longitud="maxLength" class="my-3"></PaginatePosts>
    </section>

    <section>

    <div class="row row-cols-1 row-cols-3 g-4">
      <BlogPost v-for="post in posts.slice(posInicio, posFin)" :key="post.id"
      :id="post.id"
      :title="post.title"
      :body="post.body"
      @cambiarFavoritoProp="cambiarFavoritoMethod"
      ></BlogPost>
    </div>


    </section>

  </div>

</template>