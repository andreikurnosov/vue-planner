<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <p>
          {{ project.title }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'Home',
  setup() {
    const projects = ref([])
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => (projects.value = data))
      .catch(err => console.log(err.message))
    return {
      projects
    }
  }
}
</script>
