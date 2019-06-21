<template>
  <div class="calendar-days-of-week">
    <small class="day-names" v-for="day in daysOfWeek">{{day}}</small>
  </div>
</template>

<script>
  export default{
    data: function(){
      return {
        daysOfWeek: ['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс']
      }
    }
  }
</script>

<style>
  .calendar .calendar-days-of-week{
    display: grid;
    grid-template-columns: repeat(7, 1fr); 
    border-right: 2px solid var(--border);
  }

  .calendar .calendar-days-of-week .day-names{
    text-align: center;
    width: 100%;
    border-left: 2px solid var(--border);
    border-bottom: 2px solid var(--border);
    text-transform: uppercase;
    padding: 2px;    
  }
</style>