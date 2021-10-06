<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "What is Vuex?",
          answers: [
            {
              text: "It handles state management",
              is_correct: true,
            },
            {
              text: "It's used for styling components",
              is_correct: false,
            },
            {
              text: "It assists with binding",
              is_correct: false,
            },
            {
              text: "It's an external library for API calls",
              is_correct: false,
            },
          ],
        },
        {
          q: "What lifecycle method is BEST for API calls?",
          answers: [
            {
              text: "beforeMount()",
              is_correct: false,
            },
            {
              text: "mounted()",
              is_correct: false,
            },
            {
              text: "created()",
              is_correct: true,
            },
            {
              text: "beforeCreate()",
              is_correct: false,
            },
          ],
        },
        {
          q: "What is a computed property",
          answers: [
            {
              text:
                "It's called whenever there is a change to ANY data property",
              is_correct: false,
            },
            {
              text:
                "Declaratively describes a value that depends on other values",
              is_correct: true,
            },
            {
              text: "Explicitly used to calculate the sum of two numbers",
              is_correct: false,
            },
          ],
        },
        {
          q: "What year was Vue's initial release?",
          answers: [
            {
              text: "2009",
              is_correct: false,
            },
            {
              text: "2016",
              is_correct: false,
            },
            {
              text: "2004",
              is_correct: false,
            },
            {
              text: "2014",
              is_correct: true,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 3,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 4,
          max: 4,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  font-size: 20px;
  font-family: sans-serif;
  padding-top: 20px;
  background: #e6ecf1;
}

.ctr {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
  box-sizing: border-box;
  position: relative;
}
.questions-ctr {
  position: relative;
  width: 100%;
}
.question {
  width: 100%;
  padding: 20px;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  background-color: #00ca8c;
  color: #fff;
  box-sizing: border-box;
}
.single-question {
  position: relative;
  width: 100%;
}
.answer {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: 0.2s linear all;
}
.answer span {
  display: inline-block;
  margin-left: 5px;
  font-size: 0.75em;
  font-style: italic;
}
.progress {
  height: 50px;
  margin-top: 10px;
  background-color: #ddd;
  position: relative;
}
.bar {
  height: 50px;
  background-color: #ff6372;
  transition: all 0.3s linear;
}
.status {
  position: absolute;
  top: 15px;
  left: 0;
  text-align: center;
  color: #fff;
  width: 100%;
}
.answer:not(.is-answered) {
  cursor: pointer;
}
.answer:not(.is-answered):hover {
  background-color: #8ce200;
  border-color: #8ce200;
  color: #fff;
}

.title {
  width: 100%;
  padding: 20px;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  background-color: #12cbc4;
  color: #fff;
  box-sizing: border-box;
}
.desc {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: 0.4s linear all;
  text-align: center;
}
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.3s linear;
}
.fade-leave-active {
  transition: all 0.3s linear;
  opacity: 0;
  position: absolute;
}
.fade-leave-to {
  opacity: 0;
}

.reset-btn {
  background-color: #ff6372;
  border: 0;
  font-size: 22px;
  color: #fff;
  padding: 10px 25px;
  margin: 10px auto;
  display: block;
}

.result {
  width: 100%;
}

.reset-btn:active,
.reset-btn:focus,
.reset-btn:hover {
  border: 0;
  outline: 0;
}
</style>
