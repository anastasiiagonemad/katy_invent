<template>
    <div>
      <div v-if="showIntro" class="intro">
      <div class="intro-content">
        <h2>Хотите включить музыкальное сопровождение для создания атмосферы?</h2>
        <h5>не забудьте включить звук на телефоне</h5>
        <div class="buttons">
          <button @click="handleAnswer(true)">Да</button>
          <button @click="handleAnswer(false)">Нет</button>
        </div>
      </div>
    </div>
    <div v-else>
      <Main />
    </div>
    <transition name="heart-grow">
      <div v-if="showHeart" class="heart"><img src="/images/heart-white.svg" alt="heart"></div>
    </transition>
    </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import Main from '@/components/Main.vue'
import track from '/audio/love.mp3'

const showIntro = ref(true)
const showHeart = ref(false)

const audio = new Audio(track)

const handleAnswer = (play: boolean) => {
  if (play) {
    audio.loop = true
    audio.play().catch((error) => {console.error('Ошибка воспроизведения музыка', error)})
  }

  showHeart.value = true

  setTimeout(() => {
    showIntro.value = false
    showHeart.value = false
  }, 4000)
}
</script>

<style lang="scss" scoped>
.intro {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(183, 9, 9);;
  position: absolute;
  inset: 0;

  h2 {
    color: white;
    text-align: center;
    width: 70vw;
    font-size: 5vw;
    font-weight: 100;
  }

  h5 {
    color: white;
    text-align: center;
    width: 70vw;
    font-size: 1.5vw;
    font-weight: 100;
  }

  .buttons {
    margin-top: 150px;
    display: flex;
    justify-content: space-between;
    button {
      background: none;
      border: none;
      font-size: 10vw;
      font-family: 'names';
      color: white;
      cursor: pointer;

    }
  }

}

.heart {
  position: absolute;
  display: flex;
  justify-content: center;align-items: center;
  top: 20%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 50px;
  animation: grow 5s forwards;
}

/* Анимация для сердечка */
@keyframes grow {
  0% {
    transform: scale(0.1);
  }
  25% {
    transform: scale(1.5);
  }
  50% {
    transform: scale(3);
  }
  75% {
    transform: scale(5);
  }
  100% {
    transform: scale(8);
  }
}

.heart-grow-enter-active,
.heart-grow-leave-active {
  transition: opacity 0.5s;
}
.heart-grow-enter-from,
.heart-grow-leave-to {
  opacity: 0;
}
</style>
