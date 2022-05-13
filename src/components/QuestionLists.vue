<template>
  <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-6" :class="{'hidden': !isPlaying}">
    <p class="text-2xl text-bold"> {{ Questions[index].question }}</p>

    <div v-if="Array.isArray(Questions[index].correctAnswer)">
        <label v-for="option in Questions[index].options" :key="option"  class="flex items-center gap-3 mt-4 border border-gray-300 rounded-lg py-2 px-6 text-lg cursor-pointer hover:bg-gray-200 ">
            <input type="checkbox"  :value="option" v-model="selectedAnswer" /> {{ option }}
        </label>
    </div>
    <div v-else>
        <label v-for="option in Questions[index].options" :key="option" class="flex items-center gap-3 mt-4 border border-gray-300 rounded-lg py-2 px-6 text-lg cursor-pointer hover:bg-gray-200">
            <input type="radio"  :value="option" v-model="selectedAnswer"/> {{ option }}
        </label>
    </div>

      <div v-if="Questions.length != index + 1">
            <button @click="nextQuestion" class="flex ml-auto py-2 px-8 mt-4 bg-indigo-700 rounded-md text-white hover:bg-indigo-900"> Next </button>
      </div>
      <div v-else>
            <button @click="submit" class="flex ml-auto py-2 px-8 mt-4 bg-indigo-700 rounded-md text-white hover:bg-indigo-900"> Submit </button>
      </div>
  </div>

  <Result v-show="isPlaying == false" :score="score"  :totalAnswers="totalAnswers" @playAgain="playAgain"/>
</template>

<script>
import Result from './Result.vue'

export default {
    components: {Result},
    data(){
        return{
            Questions: [
                {
                    id: 1,
                    question: "How to delete a directory in Linux?",
                    options: ["ls", "delete", "rmdir", "remove"],
                    correctAnswer: "rmdir",
                },
                {
                    id: 2,
                    question: "When was Vue3 created?",
                    options: ["2022", "2019", "2021", "2018"],
                    correctAnswer: "2021",
                },
                {
                    id: 3,
                    question: "Select technologies for frontend developer",
                    options: ["HTML", "PHP", "C++", "React"],
                    correctAnswer: ["HTML","React"],
                },
                {
                    id: 4,
                    question: "Who developed Vue?",
                    options: ["Evan Yu", "Dennis Ritchie", "Jack Dorsey", "Mark Zuckerberg "],
                    correctAnswer: "Evan Yu",
                },
            ],

            index: 0,
            score: 0,
            selectedAnswer: [],
            isPlaying: true,
            totalAnswers: 0,
        }
    },

    methods:{
        nextQuestion(){

            this.checkAnswer();

            this.selectedAnswer = [];

            this.index++;

        },

        submit(){

            this.checkAnswer();

            this.isPlaying = false;
        },

        checkAnswer(){
            if(!Array.isArray(this.Questions[this.index].correctAnswer) ){
                this.selectedAnswer == this.Questions[this.index].correctAnswer ? this.score++ : this.score;

                this.totalAnswers++;
            }else {

                this.Questions[this.index].correctAnswer.forEach(el =>{
                    this.selectedAnswer.includes(el) ? this.score++ : this.score;

                    this.totalAnswers++;
                })
            }

        },

        playAgain(){
            this.index = 0;
            this.score = 0;
            this.selectedAnswer = [];
            this.isPlaying = true;
            this.totalAnswers = 0
        }
    }
}
</script>

<style>
    input[type="radio"],
    input[type="checkbox"]{
        display: inline-block;
        width: 20px;
        height: 20px; 
    }

    input[type="radio"]:checked,
    input[type="checkbox"]:checked{
        @apply bg-gray-300;
    }
</style>