<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showHideDetails">
        {{ project.title }}
        <span class="material-icons"
          >{{ showDetails ? 'expand_less' : 'expand_more' }}
        </span>
      </h3>
      <div class="icons">
        <span class="material-icons">edit</span>
        <span class="material-icons" @click="deleteProject">delete</span>
        <span
          class="material-icons"
          :class="project.complete ? 'complete-icon' : ''"
          @click="toggleComplete"
          >done</span
        >
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  props: {
    project: {
      required: false
    }
  },
  setup(props, { emit }) {
    const showDetails = ref(false)
    const uri = ref('http://localhost:3000/projects/' + props.project.id)

    function showHideDetails() {
      showDetails.value = !showDetails.value
    }

    function deleteProject() {
      fetch(uri.value, { method: 'DELETE' })
        .then(() => emit('delete', props.project.id))
        .catch(err => console.log(err.message))
    }

    function toggleComplete() {
      fetch(uri.value, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !props.project.complete })
      })
        .then(() => {
          emit('complete', props.project.id)
        })
        .catch(err => console.log(err.message))
    }

    return {
      showHideDetails,
      showDetails,
      deleteProject,
      toggleComplete
    }
  }
}
</script>

<style scoped>
.project {
  margin: 20px auto;
  background-color: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}
.details {
  opacity: 0.7;
}

h3 {
  cursor: pointer;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  font-size: 2.4rem;
  margin-left: 1rem;
  color: #bbb;
  cursor: pointer;
}

.material-icons:hover {
  color: #777;
}

.complete-icon {
  color: #00ce89;
}

.project.complete {
  border-left: 4px solid #00ce89;
}
</style>
