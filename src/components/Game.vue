<template>
  <div class="game" :class="{'game_inactive' : !isGameStart}">
    <Cell 
      :cellId="first"
      :soundSrc="firstSrc"
      :isGameStart="isGameStart"
      :cellToClick="cellToClick"
      :computerSequence="gameplay.gameSubsequence"
      @clickCell="(i) => userSelect(i)"
    />
    <Cell 
      :cellId="second"
      :soundSrc="secondSrc"
      :isGameStart="isGameStart"
      :cellToClick="cellToClick"
      :computerSequence="gameplay.gameSubsequence"
      @clickCell="(i) => userSelect(i)"
    />
    <Cell 
      :cellId="third"
      :soundSrc="thirdSrc"
      :isGameStart="isGameStart"
      :cellToClick="cellToClick"
      :computerSequence="gameplay.gameSubsequence"
      @clickCell="(i) => userSelect(i)"
    />
    <Cell 
      :cellId="four"
      :soundSrc="fourSrc"
      :isGameStart="isGameStart"
      :cellToClick="cellToClick"
      :computerSequence="gameplay.gameSubsequence"
      @clickCell="(i) => userSelect(i)"
    />
    <div class="info">
      <p>Раунд: {{ gameplay.roundCount }}</p>
      <p :class="{lose: !isLose}">Вы проиграли</p>
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
      },
      cellToClick: '',
      isLose: false,
    }
  },
  methods: {
    chooseRandomValue() {
      const random = Math.floor(Math.random() * 4) + 1;
      if (random === 1) return 'first';
      if (random === 2) return 'second';
      if (random === 3) return 'third';
      if (random === 4) return 'four';
    },
    computerClicks(el) {
      if (el === 1) this.cellToClick = 'first';
      if (el === 2) this.cellToClick = 'second';
      if (el === 3) this.cellToClick = 'third';
      if (el === 4) this.cellToClick = 'four';
    },
    userSelect(id) {
      if (this.gameplay.turn === 'user') {
        this.gameplay.userSubsequence.push(id);
        this.gameplay.userSubsequence.forEach((el, i) => {
          if (el !== this.gameplay.gameSubsequence[i]) {
            this.$emit('lose');
            this.gameplay.roundCount = 0;
            this.gameplay.turn = 'computer';
            this.gameplay.selectedDiff = '';
            this.gameplay.gameSubsequence = [];
            this.gameplay.userSubsequence = [];
            this.isLose = true;
          }
        })
        if (this.gameplay.userSubsequence.length === this.gameplay.gameSubsequence.length && !this.isLose) {
          this.gameplay.turn = 'computer';
          this.computerSelect();
        }
      }
    },
    computerSelect() {
      if (this.gameplay.turn === 'computer') {
        this.gameplay.roundCount++;
        this.gameplay.userSubsequence = [];
        const newCellNumber = this.chooseRandomValue();
        this.gameplay.gameSubsequence.push(newCellNumber);
        this.gameplay.gameSubsequence.forEach(el => {
          this.computerClicks(el);
        })
        this.gameplay.turn = 'user';
      }
    }
  },
  watch: {
    isGameStart(value) {
      if (value) {
        this.isLose = false;
        this.computerSelect();
      }
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