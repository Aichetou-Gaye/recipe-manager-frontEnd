<template>
  <div class="container-fluid">
    <h2>{{ $t("categorie.list.titre") }}</h2>
    <div class="d-flex justify-content-end mb-4">
      <router-link to="/categorie/new" class="btn btn-danger">
        <i class="fa-solid fa-plus"></i> {{ $t("categorie.list.boutton") }}
      </router-link>
    </div>
    <div class="contact-list-table">
      <table class="table table-striped table-bordered">
        <thead>
          <tr class="table-active">
            <th scope="col">#</th>
            <th scope="col">{{ $t("categorie.list.col1") }}</th>
            <th scope="col" class="text-center">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-if="store.categories.length === 0">
            <td colspan="3" class="text-center">{{ $t("categorie.list.data") }}</td>
          </tr>
          <tr v-for="(categorie, index) in store.categories" :key="categorie.id">
            <td scope="row">{{ index + 1 }}</td>
            <td>{{ categorie.nom }}</td>
            <td class="text-center">
              <router-link :to="`/categorie/show/${categorie.id}`" class="btn btn-xs btn-success me-4">
                <i class="fa-solid fa-eye"></i>
              </router-link>
              <router-link :to="`/categorie/edit/${categorie.id}`" class="btn btn-xs btn-primary me-4">
                <i class="fa-solid fa-pen-to-square"></i>
              </router-link>
              <button @click="destroy(categorie.id)" class="btn btn-xs btn-danger">
                <i class="fa-solid fa-trash"></i>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <!-- Modal d'Aperçu -->
  <!-- <div class="modal fade" id="categoryModal" tabindex="-1" aria-labelledby="categoryModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="categoryModalLabel">{{ $t("categorie.show.titre") }}</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <p><strong>{{ $t("categorie.show.row1") }}:</strong> {{ current?.value?.nom }}</p>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">{{ $t("categorie.show.boutton")
            }}</button>
        </div>
      </div>
    </div>
  </div> -->
</template>

<script setup>
import { useCategorieStore } from '@store';
import { onMounted, ref } from 'vue';
import { useI18n } from 'vue-i18n';

const t = useI18n();
const store = useCategorieStore();
const current = ref(null);

const view = (categorie) => {
  current.value = categorie;
};

const destroy = (id) => {
  try {
    const verify = window.confirm("Etes vous sûr de vouloir supprimer cette catégorie")
    if(verify) {
      store.destroy(id)
    }
  } catch (error) {
    console.log(error.message);
    
  }
}

onMounted(() => {
  store.loadDataFromApi();
});
</script>

<style scoped>
.logo {
  width: 60px;
}

.container-fluid {
  padding: 10px 10em;
}
</style>
