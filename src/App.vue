<template>
  <div class="app" id="app">
    <Game :diff="difficulty" :isGameStart="isGameStart" />
    <form
      class="settings"
      :class="{'settings_inactive': isGameStart}"
      @submit.prevent="startGame"
    >
      <label>
        Легко
        <input type="radio" name="diff" value="easy" v-model="difficulty" :disabled="isGameStart ? true : false">
      </label>
      <label>
        Нормально
        <input type="radio" name="diff" value="medium" v-model="difficulty" :disabled="isGameStart ? true : false">
      </label>
      <label>
        Сложно
        <input type="radio" name="diff" value="hard" v-model="difficulty" :disabled="isGameStart ? true : false">
      </label>
      <button type="submit" :disabled="isGameStart ? true : false">Старт</button>
    </form>
  </div>
</template>

<script>
import Game from './components/Game.vue'

export default {
  name: 'App',
  components: {
    Game
  },
  data() {
    return {
      isGameStart: false,
      difficulty: 'easy',
    }
  },
  methods: {
    startGame() {
      this.isGameStart = true;
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .app {
    display: flex;
    flex-direction: column;
    background-color: #252525;
    min-height: 100vh;
    color: #fff;
    align-items: center;
    padding-top: 120px;
  }

  .settings {
    display: flex;
    flex-direction: column;
    row-gap: 16px;
    padding-top: 25px;
    font-size: 24px;
  }

  .settings button {
    font-size: 24px;
    border-radius: 10px;
    cursor: pointer;
  }

  .settings label {
    cursor: pointer;
  }

  .settings input {
    cursor: pointer;
  }

  .settings_inactive {
    opacity: .5;
  }

  .settings_inactive button {
    cursor: default;
  }

  .settings_inactive label {
    cursor: default;
  }

  .settings_inactive input {
    cursor: default;
  }
</style>
