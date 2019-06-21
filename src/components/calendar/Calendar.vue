<template>
  <div class="calendar">
    <CalendarHeader :date="current" @monthChange="onMonthChange"/>
    <CalendarWeekDays />

    <div class="calendar-days-of-month">
      <div class="previous days" v-for="day in daysOfPreviousMonth">{{day}}</div>
      <div class="current days" v-for="day in daysOfMonth" :style="{'background-color': backgroundColor(day)}" @click="select(day)" :class="{ selected: isSelected(day) }">{{day}}</div>
      <div class="next days" v-for="day in daysOfNextMonth">{{day}}</div>
    </div>
  </div>
</template>

<script>
import CalendarHeader from './CalendarHeader.vue'
import CalendarWeekDays from './CalendarWeekDays.vue'

export default {  
  components: {
    CalendarHeader,
    CalendarWeekDays
  },

  props: {
    date: {
      type: Date,
      default: new Date()
    },
    events: Array
  },

  data: function(){
    return {
      current: new Date(),
      selected: null
    }
  },

  created: function(){
    this.current = this.date;
  },

  methods: {
    onMonthChange: function(date){
      this.current = date;
      this.selected = null;
      this.$emit('monthChange', date.getMonth() + 1);
    },

    backgroundColor: function(day){
      let color = 'white';
      let date = formatDate(new Date(this.current.getFullYear(), this.current.getMonth(), day));

      this.events.forEach(event => {
        if (formatDate(event.date) == date) {
          color = event.color
        }
      })
      return color;
    },
    
    select: function(day){
      this.selected = new Date(this.current.getFullYear(), this.current.getMonth(), day);
      this.$emit('select', this.selected);
    },

    isSelected: function(day){
      if (!this.selected) return false;
      return this.selected.getDate() == day;
    }
  },

  computed: {
    daysOfPreviousMonth: function(){
      let weekDay = getWeekDay(getFirstDay(this.current));
      let lastDay = getMonthDays(getPreviousMonth(this.current));
      return getArrayInRange(lastDay - weekDay + 2, lastDay);
    },

    daysOfMonth: function(){
      return getArrayInRange(1, getMonthDays(this.current));
    },

    daysOfNextMonth: function(){
      let weekDay = getWeekDay(getLastDay(this.current));
      return getArrayInRange(1, 7 - weekDay);
    },    

  }
}

let getWeekDay = d => d.getDay() || 7;

let getLastDay = d => new Date(d.getFullYear(), d.getMonth() + 1, 0);
let getFirstDay = d => new Date(d.getFullYear(), d.getMonth(), 1);
let getPreviousMonth = d => new Date(d.getFullYear(), d.getMonth() - 1, d.getDate());
let getMonthDays = (d) => new Date(d.getFullYear(), d.getMonth() + 1, 0).getDate();
let formatDate = d => (d.getFullYear() + '.' + d.getMonth() + '.' + d.getDate());

let getArrayInRange = function(start, finish){
  if (start > finish) return [];
  return (new Array(finish - start + 1)).fill(0).map((d, index) => index + start)
}

</script>

<style>
  .calendar{
    border: 2px solid var(--border);
  }
  .calendar .calendar-days-of-month{
    display: grid;
    grid-template-columns: repeat(7, 1fr); 
    border-right: 2px solid var(--border);  
    grid-template-rows: repeat(5, 1fr); 
  }

  .calendar .calendar-days-of-month .days{
    text-align: center;
    width: 100%;
    border-left: 2px solid var(--border);
    border-bottom: 2px solid var(--border);

    padding: 0.4rem 0;
  }

  .calendar .calendar-days-of-month .days.previous, .calendar .calendar-days-of-month .days.next{
    color: lightgray;
  }
  .calendar .calendar-days-of-month .days.current:hover{
    background-color: red !important;
    color: white;
    cursor: pointer;
  }
  .calendar .selected{
    background-color: red !important;
    color: white;
  }

  @media (min-width: 768px) {
    .calendar .calendar-days-of-month .days{
      padding: 0.6rem 0;
    }
  }
</style>
