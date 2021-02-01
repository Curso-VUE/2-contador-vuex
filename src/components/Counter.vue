<template>
  <div class="container">
    <button
      class="btn btn-success btn-block"
      @click="increment"
    >
      Incrementar
    </button>
    <div class="alert alert-secondary text-center mt-3">
      {{ counter }}
    </div>
    <button
      class="btn btn-danger btn-block"
      @click="decrement"
    >
      Decrementar
    </button>
  </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex'
export default {
  computed: {
    ...mapState(['counter']),
  },
  methods: {
    ...mapMutations(['increment', 'decrement'])
  }  
}
</script>
