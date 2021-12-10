<template>
  <div>
    <div class="container">
      <h1>The Voice App</h1>
      <select>
        <option v-for="(voice, index) in voices" :key="index" :name="voice.name">
         {{ voice.name }} ({{ voice.lang }})
        </option>
      </select>
      <label for="rate"></label>
      <input type="range" name="rate" min="0" max="3" value="1" step="0.1">

      <label for="pitch"></label>
      <input type="range" name="pitch" min="0" max="2"  step="0.1">

      <textarea ref="text">Hi! Vue</textarea>

      <div class="button-group">
        <button class="stop">Stop</button>
        <button class="speak">Speak</button>
      </div>
    </div>
  </div>
</template>

<script>
import {ref, onMounted} from 'vue';
export default {

  setup() {
    const text = ref(null);
    let voices = [];
    

    const msg = new SpeechSynthesisUtterance();
    const synthesis =  window.speechSynthesis;


    onMounted(() => {
      msg.text = text.value.value;
      console.log(msg);
      synthesis.onvoiceschanged = () => {
        voices = synthesis.getVoices();
        console.log(voices);
      }
    });
    
    
    return{
      msg,
      voices,
      text,
      synthesis,
    }
    
  }
  
}
</script>


