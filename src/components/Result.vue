<template>
  <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-6">
      <h2 class="font-bold text-indigo-700 text-center text-2xl">Your score : {{ score }} out of {{ totalAnswers }}</h2>

       <button @click="playAgain" class="flex m-auto py-2 px-8 mt-6 bg-indigo-700 rounded-md text-white hover:bg-indigo-900"> Try Again </button>
  </div>
</template>

<script>
export default {
    props:['score', 'totalAnswers'],

    methods: {
        playAgain(){
            this.$emit('playAgain');
        }
    }
}
</script>

<style>

</style>