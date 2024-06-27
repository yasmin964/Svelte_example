<template>
    <div class="box_vacancy">
      <h3 class="vac_data">{{ vacancy.name }}</h3>
      <p>{{ vacancy.description }}</p>
      <!-- Добавьте другие поля, которые вы хотите отобразить здесь -->
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, PropType } from 'vue';
  
  interface Vacancy {
    id: number;
    name: string;
    description: string;
    // добавьте другие поля, если необходимо
  }
  
  export default defineComponent({
    name: 'VacancyBox',
    // это способ передачи данных от родительского компонента к дочернему компоненту в Vue.js.
    props: {
      vacancy: {
        type: Object as PropType<Vacancy>,
        required: true
      }
    }
  });
  </script>
  
  <style scoped>
  .box_vacancy {
    padding: 20px;
    border: 1px solid #ddd;
    margin-bottom: 20px;
    background-color: #fff;
  }
  
  .vac_data {
    color: blue;
  }
  </style>
  