<template>
  <div class="flex w-full h-screen justify-center items-center">
    <div class="w-full max-w-xl">
      <h1 class="font-bold text-5xl text-center text-indigo-700">
        Simple Quiz
      </h1>

      <QuestionList />
    </div>
  </div>
</template>

<script>
import QuestionList from './components/QuestionLists.vue'
export default {
  name: 'App',

  components: {
    QuestionList
  }
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  @apply text-gray-700 bg-gray-100;
}
</style>
