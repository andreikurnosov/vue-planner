<template>
  <div class="project">
    <div class="actions">
      <h3 @click="showHideDetails">
        {{ project.title }}
      </h3>
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
  setup() {
    const showDetails = ref(false)

    function showHideDetails() {
      showDetails.value = !showDetails.value

      console.log(showDetails.value)
    }

    return {
      showHideDetails,
      showDetails
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
  opacity: .7;
}

h3 {
  cursor: pointer;
}
</style>
