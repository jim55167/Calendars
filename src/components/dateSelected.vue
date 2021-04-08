<template>
  <div class="selected-box">
    <div class="date-selected">
      <span @click="selectedPre"><i class="fas fa-arrow-left"></i></span>
      <span @click="selectedCurrent">Today</span>
      <span @click="selectedNext"><i class="fas fa-arrow-right"></i></span>
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  name: 'pointer',
  props: {
    currentDate: {
      type: String,
      required: true
    },
    selectedDate: {
      type: Object,
      required: true
    }
  },
  methods: {
    selectedPre () {
      const newDate = dayjs(this.selectedDate).subtract(1, 'month')
      this.$emit('dateSelected', newDate)
    },
    selectedCurrent () {
      const newDate = dayjs(this.currentDate)
      this.$emit('dateSelected', newDate)
    },
    selectedNext () {
      const newDate = dayjs(this.selectedDate).add(1, 'month')
      this.$emit('dateSelected', newDate)
    }
  }
}
</script>
