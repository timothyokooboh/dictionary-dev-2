<template>
  <div>
    <app-header></app-header>
    <transition name="animate" mode="out-in">
      <router-view/>
    </transition>
  </div>
</template>
<script>
import Header from './components/Header'
export default {
  components: {
    appHeader: Header
  }
}
</script>

<style lang="scss">
   * {
    box-sizing: border-box;
  }
  :root {
    font-size: 62.5%;
  }
  body {
    margin: 0px;
    overflow-y: scroll;
    -ms-overflow-style: none;
    font-family: 'Source Sans Pro', sans-serif;
    letter-spacing: 1.08px;
    font-size: 1.6rem;
  }
  body::-webkit-scrollbar {
    display: none;
  }
  .animate-enter-active {
    animation: animate-in 1s ease-out forwards;
  }
  .animate-leave-active {
    animation: animate-out 50ms ease-out forwards;
  }
  @keyframes animate-in {
    from {
      opacity: 0;
      transform: translateY(-30px);
    }
    to {
      opacity: 1;
      transform: translateY(0px)
    }
  }

  @keyframes animate-out {
    from {
      opacity: 1;
      transform: translateY(0px);
    }
    to {
      opacity: 0;
      transform: translateY(-30px)
    }
  }
</style>
