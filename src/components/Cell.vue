<template>
  <div
    class='cell'
    :id="cellId"
    :class="{ 'cell_active': isActive }"
    @click="light"
  >
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: ['cellId', 'soundSrc', 'isGameStart', 'canUserClick', 'delay'],
  data() {
    return {
      isActive: false,
    }
  },
  methods: {
    light() {
      if (this.isGameStart && this.canUserClick) {
        setTimeout(() => this.isActive = false, 200);
        this.isActive = true;
        const sound = new Audio(this.soundSrc);
        sound.play();
        this.$emit('clickCell', this.cellId);
      }
    },
    show() {
      setTimeout(() => this.isActive = false, this.delay * 1);
      this.isActive = true;
      const sound = new Audio(this.soundSrc);
      sound.play();
    }
  },
}
</script>

<style>
  .cell {
    width: 45vw;
    height: 45vw;
    cursor: pointer;
    max-width: 200px;
    max-height: 200px;
    opacity: .2;
  }

  .cell_active {
    opacity: 1;
  }

  #first {
    border-radius: 100% 0 0 0;
    background-color: aqua;
  }

  #second {
    border-radius: 0 100% 0 0;
    background-color: red;
  }

  #third {
    border-radius: 0 0 0 100%;
    background-color: yellow;
  }

  #four {
    border-radius: 0 0 100% 0;
    background-color: green;
  }
</style>