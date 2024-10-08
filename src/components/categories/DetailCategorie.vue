<template>
  <div class="container">
    <router-link to="/categorie" class="btn btn-success m-2">
      <i class="fa-solid fa-arrow-left"></i>
    </router-link>
    <div>
      <h2 class="text-center">{{ $t("categorie.show.titre") }}</h2>
      <p class="bg-success fw-bold p-2"><span class="text-white ">Nom de la categorie : </span>{{ categorie?.nom }}</p>
      <div class="row">
        <div class="col-md-4 mb-3" v-for="(recipe, index) in recipes" :key="index">
          <div class="card">
            <div class="card-header"><span class="fw-bold">Recette : </span>{{ recipe.titre }}</div>
            <div class="card-body shadow-lg">
              <h5 class="card-title text-"><span class="fw-bold">Type : </span> {{ recipe.type }}</h5>
              <p class="card-text"><span class="fw-bold">Ingredients : </span> {{ recipe.ingredients }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { useCategorieStore } from '@store';
import { useI18n } from 'vue-i18n';

const t = useI18n();
const route = useRoute();
const store = useCategorieStore();
const id = route.params.id;
const categorie = ref(null);
const recipes = ref(null)


onMounted(async () => {
  try {
    categorie.value = await store.getById(id)
    recipes.value = await store.recipes(id)
  } catch (error) {
    console.log(error);
  }
});
</script>

<style scoped></style>