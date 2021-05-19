<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">
      View All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ['current'],
  setup(props, { emit }) {
    
    function updateFilter(by) {
      emit('filterChange', by)
    }

    return {
      updateFilter
    }
  }
}
</script>

<style scoped>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}

.filter-nav button.active {
  color: rgb(68, 68, 68);
}
</style>
