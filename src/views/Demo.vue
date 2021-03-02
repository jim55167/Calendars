<template>
  <div>
    <div class="demo-month">
      <div class="month-header">
        <Pointer
          :selected-date = "selectedDate"
        />
        <DateSelected
          :current-date="today"
          :selected-date="selectedDate"
          @dateSelected="selDate"
        />
      </div>
        <WeekDate/>
        <ol class="grid">
          <MonthDate
            v-for="day in days"
            :key="day.date"
            :day="day"
            :is-today="day.date === today"
          />
        </ol>
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
import Pointer from '@/components/pointer'
import DateSelected from '@/components/dateSelected'
import MonthDate from '@/components/monthDate'
import WeekDate from '@/components/weekDate'
import weekday from 'dayjs/plugin/weekday'
import weekOfYear from 'dayjs/plugin/weekOfYear'

dayjs.extend(weekday)
dayjs.extend(weekOfYear)

export default {
  name: 'Demo',
  data () {
    return {
      selectedDate: dayjs()
    }
  },
  methods: {
    getWeekday (date) {
      return dayjs(date).weekday()
    },
    selDate (newDate) {
      this.selectedDate = newDate
      console.log(newDate)
    }
  },
  computed: {
    today () {
      return dayjs().format('YYYY-MM-DD')
    },
    month () {
      return Number(this.selectedDate.format('M'))
    },
    year () {
      return Number(this.selectedDate.format('YYYY'))
    },
    getMonth () {
      return dayjs(this.selectedDate).daysInMonth()
    },
    currentDays () {
      // console.log(this.selectedDate)
      return [...Array(this.getMonth)].map((day, index) => {
        return {
          date: dayjs(`${this.year}-${this.month}-${index + 1}`).format('YYYY-MM-DD'),
          isMonth: true
        }
      })
    },
    nextmonthDay () {
      const nextWeek = this.getWeekday(`${this.year}-${this.month}-${this.currentDays.length}`)
      // console.log('月底星期 :', nextWeek)
      const nextMonth = dayjs(`${this.year}-${this.month}`).add(1, 'month')
      // console.log(nextMonth)
      const nextOfmonth = nextWeek ? 7 - nextWeek : nextWeek
      // console.log('剩餘 :', nextOfmonth, '格')
      return [...Array(nextOfmonth)].map((day, index) => {
        return {
          date: dayjs(`${nextMonth.year()}-${nextMonth.month() + 1}-${index + 1}`).format('YYYY-MM-DD'),
          isMonth: false
        }
      })
    },
    premonthDate () {
      const firstWeek = this.getWeekday(this.currentDays[0].date)
      // console.log('星期 :', firstWeek)
      const prevMonth = dayjs(`${this.year}-${this.month}`).subtract(1, 'month')
      const lastMonth = firstWeek ? firstWeek - 1 : 6
      // console.log('空 :', lastMonth, '格')
      const prefirstDay = dayjs(this.currentDays[0].date).subtract(lastMonth, 'day').date()
      // console.log('第一格日期 :', prefirstDay, '號')
      return [...Array(lastMonth)].map((day, index) => {
        return {
          date: dayjs(`${prevMonth.year()}-${prevMonth.month() + 1}-${prefirstDay + index}`).format('YYYY-MM-DD'),
          isMonth: false
        }
      })
    },
    days () {
      return [
        ...this.premonthDate,
        ...this.currentDays,
        ...this.nextmonthDay
      ]
    }
  },
  components: {
    Pointer,
    DateSelected,
    MonthDate,
    WeekDate
  }
}

</script>
