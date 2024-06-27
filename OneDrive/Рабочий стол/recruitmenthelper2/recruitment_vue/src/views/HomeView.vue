<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Добро пожаловать в RecruitmentInno
        </p>
        <p class="subtitle">
          Вакансии/Специалисты
        </p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="title" style="color: blue;">Последние вакансии</h2>
      </div>
      <VacancyBox 
        v-for="vacancy in latestVacancies" 
        :key="vacancy.id" 
        :vacancy="vacancy" 
        class="column is-4"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import VacancyBox from '@/components/VacancyBox.vue'; // Импорт дочернего компонента

interface Vacancy {
  id: number;
  name: string;
  description: string;
  // добавьте другие поля, если необходимо
}

export default defineComponent({
  name: 'HomeView',
  components: {
    VacancyBox // Регистрация дочернего компонента
  },
  data() {
    return {
      latestVacancies: [] as Vacancy[]
    }
  },
  mounted() {
    this.getLatestVacancies();
    document.title = 'Home | Djackets';
  },
  methods: {
    async getLatestVacancies() {
      try {
        const response = await axios.get('main/');
        this.latestVacancies = response.data as Vacancy[];
      } catch (error) {
        console.error(error);
      }
    }
  }
});
</script>

<style scoped>
.home {
  background-color: pink /* Светло-серый фон */
}
</style>
