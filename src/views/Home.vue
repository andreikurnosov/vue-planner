<template>
  <div class="home">
    <filter-nav @filterChange="current = $event" :current="current" />
    <div v-if="projects">
      <div v-for="project in filteredProjects" :key="project.id">
        <project-item
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { computed, ref } from 'vue'
import ProjectItem from '../components/ProjectItem.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  components: { ProjectItem, FilterNav },

  name: 'Home',
  setup() {
    const projects = ref([])
    const current = ref('all')

    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => (projects.value = data))
      .catch(err => console.log(err.message))

    function handleDelete(id) {
      projects.value = projects.value.filter(project => {
        return project.id !== id
      })
    }

    function handleComplete(id) {
      let p = projects.value.find(project => {
        return project.id === id
      })

      p.complete = !p.complete
    }

    const filteredProjects = computed(() => {
      if (current.value === 'completed') {
        return projects.value.filter(project => project.complete)
      }

      if (current.value === 'ongoing') {
        return projects.value.filter(project => !project.complete)
      }

      if (current.value === 'all') {
        return projects.value
      }
    })

    return {
      projects,
      handleDelete,
      handleComplete,
      current,
      filteredProjects
    }
  }
}
</script>
