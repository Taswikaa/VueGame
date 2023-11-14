<template>
  <div class="game" :class="{'game_inactive' : !isGameStart}">
    <Cell 
      :cellId="first"
      :soundSrc="firstSrc"
      @clickCell="(i) => userSelect(i)" 
    />
    <Cell 
      :cellId="second"
      :soundSrc="secondSrc"
      @clickCell="(i) => userSelect(i)" 
    />
    <Cell 
      :cellId="third"
      :soundSrc="thirdSrc"
      @clickCell="(i) => userSelect(i)" 
    />
    <Cell 
      :cellId="four"
      :soundSrc="fourSrc"
      @clickCell="(i) => userSelect(i)" 
    />
    <div class="info">
      <p>Раунд: {{ gameplay.roundCount }}</p>
      <p class="lose">Вы проиграли</p>
    </div>
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
  props: ['diff', 'isGameStart'],
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
      gameplay: {
        gameSubsequence: [],
        userSubsequence: [],
        selectedDiff: '',
        roundCount: 0,
        turn: 'computer',
      }
    }
  },
  methods: {
    chooseRandomValue() {
      return Math.floor(Math.random() * 4) + 1;
    },
    userSelect(id) {
      if (this.gameplay.turn === 'user') {
        console.log('input' ,id);
        this.gameplay.turn = 'computer';
        this.computerSelect();
      }
    },
    computerSelect() {
      if (this.gameplay.turn === 'computer') {
        this.gameplay.roundCount++;
        const newCellNumber = this.chooseRandomValue();
        this.gameplay.gameSubsequence.push(newCellNumber);
        for (let i = 0; i < this.gameplay.gameSubsequence.length; i++) {
          console.log('Игра', this.gameplay.gameSubsequence[i]);
        }
        this.gameplay.turn = 'user';
      }
    }
  },
  watch: {
    isGameStart() {
      this.computerSelect();
    }
  }
}
</script>

<style>
  .game {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    position: relative;
  }

  .game_inactive {
    opacity: .3;
  }

  .game_inactive div {
    cursor: default;
  }

  .info {
    font-size: 24px;
    position: absolute;
    top: -100px;
    left: 25%;
    display: flex;
    flex-direction: column;
    row-gap: 10px;
    text-align: center;
  }

  .lose {
    display: none;
  }

  @media (min-width: 1024px) {
    .info {
      top: 20px;
      left: 450px;
      font-size: 32px;
      text-align: left;
      row-gap: 15px;
      min-width: 200px;
    }
  }
</style>