<template>
  <div>
    <div class="container" >
      <div class="input-container"  >
        <p>Create a countdown!</p>
        <form  class="form" @submit.prevent="updateCountdown">
          <label for="title">Title</label>
          <input type="text" class="title" placeholder="what are you counting down to?">
          <label for="date-picker">Select a date</label>
          <input type="date" class="date-picker" :min="today">
          <button type="submit" >Submit</button>
        </form>
      </div>

      <div class="countdown">
          <p class="countdown-title"></p>
          <ul>
          <li><span class="days"></span>Days</li>
          <li><span class="hours"></span>Hours</li>
          <li><span class="minutes"></span>Minutes</li>
          <li><span class="seconds"></span>Seconds</li>
          </ul>
          <button class="countdown-button">Reset</button>
      </div> 

      <div class="complete" >
        <h1 class="complete-title">Countown complete!</h1>
        <p class="complete-info">Countdown Finished on 05-05-2020</p>
        <button class="complete-button">New Countdown</button>
      </div> 
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'
export default {
  name: 'Countdown', 
  
  
  setup() {
    const today = ref(new Date().toISOString().split('T')[0])
    let countDownTitle = ref("");
    let countDownDate = ref("");
    let countDownValue;


    const second = ref(1000);
    const minute = second.value * 60;
    const hour = minute * 60;
    const day = hour * 24;


    

    const updateCountdown = (e) => {
      countDownTitle = e.srcElement[0].value;
      countDownDate = e.srcElement[1].value;
      countDownValue = new Date(countDownDate).getTime();
      console.log(countDownTitle, ",",  countDownValue)
      
      const now = new Date().getTime();
      const distance = countDownValue - now;
      console.log('distance:', distance);

      const days = Math.floor(distance / day);
      const hours = Math.floor((distance % day) / hour);
      const minutes = Math.floor((distance % hour) / minute);
      const seconds = Math.floor((distance % minutes) / second.value);
      console.log(days, hours, minutes, seconds);

      // Populate Countdown
      document.querySelector(".countdown-title").textContent = countDownTitle;
      document.querySelector(".days").textContent = days;
      document.querySelector(".hours").textContent = hours;
      document.querySelector(".minutes").textContent = minutes;
      document.querySelector(".seconds").textContent = seconds;

      // Hide Input
      document.querySelector(".input-container").style.display = "none";
      // Show CountDown
      document.querySelector(".countdown").style.display = "block";

    }

    return{
      today,
      countDownTitle,
      countDownDate,
      countDownValue,
      second,
      minute,
      hour,
      day,
      updateCountdown,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
