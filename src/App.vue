<template>
  <div>
    <nav class="navbar navbar-expand bg-dark fixed-top">
      <div class="container">
        <router-link to="/" class="navbar-brand">
          <img src="/src/assets/recipeLogo.jpg" alt="Logo" class="logo">
        </router-link>
        <div class="collapse navbar-collapse">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link to="/recette" class="nav-link text-white" activeClass="active">{{ $t("home.title1") }}</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/categorie" class="nav-link text-white" activeClass="active">{{ $t("home.title2") }}</router-link>
            </li>
          </ul>
        </div>

        <div class="d-flex">
          <select id="langue" class="form-select form-select-sm bg-dark text-white border-0" @change="changeLanguage">
            <option value="en">En</option>
            <option value="fr">Fr</option>
          </select>
        </div>
      </div>
    </nav>
    <div class="content mt-5 pt-5">
      <router-view />
    </div>
  </div>
</template>

<script setup>
import { useI18n } from 'vue-i18n';
const t = useI18n();
const { locale } = useI18n();

function changeLanguage(event) {
  locale.value = event.target.value;
}

</script>

<style scoped>
.logo {
  height: 40px;
  width: auto;
}
.active{
  font-weight: 600;
  border-bottom: 3px solid rgb(165, 164, 164);
  color: black;
  border-radius: 10px;
}

.content {
  padding-top: 70px; 
}
</style>
