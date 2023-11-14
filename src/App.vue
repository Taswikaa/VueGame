<template>
  <div class="app" id="app">
    <Game />
    <div class="info">
      <p>Раунд: 10</p>
      <p class="lose">Вы проиграли</p>
    </div>
    <form class="settings settings_inactive">
      <label>
        Легко
        <input type="radio" name="diff">
      </label>
      <label>
        Нормально
        <input type="radio" name="diff">
      </label>
      <label>
        Сложно
        <input type="radio" name="diff">
      </label>
      <button type="submit">Старт</button>
    </form>
  </div>
</template>

<script>
import Game from './components/Game.vue'

export default {
  name: 'App',
  components: {
    Game
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
    position: relative;
  }

  .info {
    font-size: 24px;
    position: absolute;
    top: 25px;
    display: flex;
    flex-direction: column;
    row-gap: 10px;
    text-align: center;
  }

  .settings {
    display: flex;
    flex-direction: column;
    row-gap: 16px;
    padding-top: 25px;
    font-size: 24px;
  }

  .settings_inactive {
    opacity: .5;
  }

  .settings button {
    font-size: 24px;
    border-radius: 10px;
  }

  .settings label {
    cursor: pointer;
  }

  .lose {
    display: none;
  }

  @media (min-width: 1024px) {
    .info {
      right: 60px;
      top: 120px;
      font-size: 32px;
      text-align: left;
      row-gap: 15px;
      min-width: 200px;
    }
  }
</style>
