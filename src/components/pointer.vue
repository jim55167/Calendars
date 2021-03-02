<template>
  <div>
    <div class="pointer">{{ selectedMonth }}</div>
  </div>
</template>

<script>

export default {
  name: 'pointer',
  props: {
    selectedDate: {
      type: Object,
      required: true
    }
  },
  computed: {
    selectedMonth () {
      return this.selectedDate.format('MMMM YYYY')
    }
  }
}
</script>
