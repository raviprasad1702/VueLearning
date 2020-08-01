<template>
  <section class="text-gray-700 body-font overflow-hidden">
    <div class="container max-w-6xl px-5 py-16 mx-auto">
      <div class="flex flex-wrap -m-12">
        <div class="p-12 md:w-full flex flex-col items-start">
          <h2
            class="sm:text-3xl text-2xl title-font font-medium text-gray-900 mt-4 mb-4"
          >
            {{ currentQuestion.question }}
          </h2>
          <ul
            class="flex flex-col w-full justify-center items-center flex-wrap"
          >
            <li
              v-for="(answer, index) in answers"
              :key="index"
              @click="selectedAnswer(index)"
              class="px-4 py-2 border-2 rounded-md hover:bg-blue-200 cursor-pointer my-2 border-blue-200 w-4/12 text-left"
              :class="answerClass(index)"
            >
              {{ answer }}
            </li>
          </ul>
          <div
            class="flex items-center flex-wrap pb-4 mb-4 border-b-2 border-gray-200 mt-auto w-full"
          ></div>
          <div class="flex gap-6">
            <button
              class="flex justify-center items-center text-white w-32 bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded"
              @click="submitAnswer()"
              :class="
                selectedIndex === null || answered
                  ? 'opacity-50 cursor-not-allowed'
                  : ''
              "
            >
              Submit
            </button>
            <button
              @click="next"
              class="flex justify-center items-center text-white w-32 bg-teal-500 border-0 py-2 px-6 focus:outline-none hover:bg-teal-600 rounded"
            >
              Next
              <svg
                fill="none"
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                class="w-4 h-4 ml-2"
                viewBox="0 0 24 24"
              >
                <path d="M5 12h14M12 5l7 7-7 7" />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffeledAnswers: [],
      answered: false,
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffelAnswer();
      },
    },
  },
  methods: {
    selectedAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;

      this.increment(isCorrect);
    },
    shuffelAnswer() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      this.shuffeledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffeledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    answerClass(index) {
      let ansClass = "";

      if (!this.answered && this.selectedIndex === index) {
        ansClass = "bg-blue-200";
      } else if (this.answered && this.correctIndex === index) {
        ansClass = "bg-green-300";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        ansClass = "bg-red-300";
      }

      return ansClass;
    },
  },
};
</script>
