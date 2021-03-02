<template>
  <div>
    <li class="date" :class="{'current': !day.isMonth, 'today': isToday}">
      <span>{{ isTag }}</span>
    </li>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  name: 'monthDate',
  props: {
    day: {
      type: Object,
      required: true
    },
    isMonth: {
      type: Boolean,
      default: false
    },
    isToday: {
      type: Boolean,
      default: false
    }
  },

  computed: {
    isTag () {
      // console.log(this.day.date)
      return dayjs(this.day.date).format('D')
    }
  }
}
</script>
