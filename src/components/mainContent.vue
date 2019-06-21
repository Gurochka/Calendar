<template>
  <main class="mt-3 ml-3">
    <Calendar :date="dateToDisplay" :events="events" @select="onSelectDate" @monthChange="onMonthChange"/>
  </main>
</template>

<script>
import Calendar from '@/components/calendar/Calendar.vue'
import events from '../assets/events.json'

export default {
  components: {
    Calendar
  },
  data: function(){
    return {
      dateToDisplay: new Date(2018, 3, 20),
      events: []
    }
  },
  created: function(){
    events.forEach(event => {
      let parsed = event.date.split('.').map(d => parseInt(d, 10));
      event.date = new Date(parsed[2], parsed[1] - 1, parsed[0]);
    })
    this.events = events;
  },
  methods: {
    onSelectDate: function(date){
      console.log('selected date: ', date)
    },
    onMonthChange: function(month){
      console.log('Month get changed', month);
    }
  }
}
</script>
<style>
  main{
    width: 30%;
  }
</style>
