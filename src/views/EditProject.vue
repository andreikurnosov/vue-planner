<template>
  <form>
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
    <button>Update Project</button>
  </form>
</template>

<script>
import { ref } from 'vue'
export default {
  props: ['id'],
  setup(props) {
    const title = ref('')
    const details = ref('')
    const uri = ref('http://localhost:3000/projects/' + props.id)

    fetch(uri.value)
      .then(res => res.json())
      .then(data => {
        title.value = data.title
        details.value = data.details
      })

    return {
      title,
      details
    }
  }
}
</script>

<style scoped>
form {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 1px 1px 2px grey;
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
  outline: none;
}

textarea {
  border: 1px solid #ddd;
  border-radius: 7px;
  padding: 1rem;
  width: 100%;
  box-sizing: border-box;
  height: 10rem;
  outline: none;
}

form button {
  transition: all 200ms;
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 1rem;
  border: 0;
  border-radius: 6px;
  font-size: 1.6rem;
}
button:hover {
  background: #00a56e;
}
</style>
