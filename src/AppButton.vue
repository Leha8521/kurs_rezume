<template>
   <button
   class="btn"
   :class="color"
   @click="$emit('load')"
    ><slot />
    </button>
</template>

<script>
export default {
  emits: ['load'],
  props: {
    color: {
      type: String,
      default: '',
      validator (value) {
        return ['', 'primary'].includes(value)
      }
    }
  }
}
</script>

<style>

</style>
