<template>
  <div class="game">
    <Cell 
      :cellId="first"
      :soundSrc="firstSrc" 
    />
    <Cell 
      :cellId="second"
      :soundSrc="secondSrc" 
    />
    <Cell 
      :cellId="third"
      :soundSrc="thirdSrc" 
    />
    <Cell 
      :cellId="four"
      :soundSrc="fourSrc" 
    />
  </div>
</template>

<script>
import Cell from './Cell.vue';
import firstSrc from '../sounds/first.mp3';
import secondSrc from '../sounds/second.mp3';
import thirdSrc from '../sounds/third.mp3';
import fourSrc from '../sounds/four.mp3';

export default {
  name: 'Game',
  components: {
    Cell
  },
  data() {
    return {
      first: 'first',
      second: 'second',
      third: 'third',
      four: 'four',
      firstSrc: firstSrc,
      secondSrc: secondSrc,
      thirdSrc: thirdSrc,
      fourSrc: fourSrc,
    }
  }
}
</script>

<style>
  .game {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }
</style>