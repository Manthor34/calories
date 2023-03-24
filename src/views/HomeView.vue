<template>
  <health-form />
</template>

<script lang="ts">
import { defineComponent } from 'vue';

// Components
import HealthForm from '../components/HealthForm.vue';

export default defineComponent({
  name: 'HomeView',

  components: {
    HealthForm,
  },
});
</script>
