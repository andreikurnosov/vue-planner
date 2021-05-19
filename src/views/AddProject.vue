<template>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title:</label>
    <input v-model="title" id="title" type="text" required />

    <label for="details">Details</label>
    <textarea
      v-model="details"
      id="details"
      required
      cols="30"
      rows="10"
    ></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {
    const title = ref('')
    const details = ref('')

    function handleSubmit() {
      console.log(title.value, details.value)
    }

    return {
      title,
      details,
      handleSubmit
    }
  }
}
</script>

<style scoped>
form {
  background: white;
  padding: 2rem;
  border-radius: 10px;
}

label {
  display: block;
  color: rgb(46, 46, 46);
  text-transform: uppercase;
  font-size: 1.4rem;
  font-weight: bold;
  letter-spacing: 3px;
  margin: 2rem 0 1rem 0;
}

input {
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 7px;
  width: 100%;
  box-sizing: border-box;
}

textarea {
  border: 1px solid #ddd;
  border-radius: 7px;;
  padding: 1rem;
  width: 100%;
  box-sizing: border-box;
  height: 10rem;
}

form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 1rem;
  border: 0;
  border-radius: 6px;
  font-size: 1.6rem;
}
</style>
