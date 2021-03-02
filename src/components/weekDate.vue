<template>
  <div>
    <ol class="week">
      <li v-for="weekday in weekDates" :key="weekday">{{ weekday }}</li>
    </ol>
  </div>
</template>

<script>
const week = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
export default {
  name: 'weekDate',

  computed: {
    weekDates () {
      return week
    }
  }
}
</script>
