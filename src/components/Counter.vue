<template>
  <div class="container">
    <button
      class="btn btn-success btn-block"
      @click="$store.commit('increment')"
    >
      Incrementar
    </button>
    <div class="alert alert-secondary text-center mt-3">
      {{ $store.state.counter }}
    </div>
    <button
      class="btn btn-danger btn-block"
      @click="$store.commit('decrement')"
    >
      Decrementar
    </button>
  </div>
</template>

<script>
export default {
  
}
</script>
