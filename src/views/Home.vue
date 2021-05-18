<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <project-item :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import ProjectItem from '../components/ProjectItem.vue'

export default {
  components: { ProjectItem },

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
