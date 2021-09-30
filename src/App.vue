<template>
  <div class="mainDiv">
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="questionArea">
      <div v-for="(question, index) in questions" :key="index">
        <QuestionTemplate
          v-if="currentQuestion == index || isResultPage"
          :question="question"
          :questionIndex="index"
          :isResultPage="isResultPage"
          @selected-answer="SetQuestionAnswer"
        />
      </div>
      <div class="buttons">
        <Button
          text="Reset"
          action="-clicked"
          @reset-clicked="ResetCurrentQuestion"
        />
        <Button
          :text="questions.length - 1 == currentQuestion ? 'Finish' : 'Next'"
          action="-clicked"
          @next-clicked="IncreaseCurrentQuestion"
          @finish-clicked="OpenResultPage"
        />
      </div>
    </div>
  </div>
</template>

<script>
import QuestionTemplate from "./components/QuestionTemplate.vue";
import Button from "./components/Button.vue";

export default {
  name: "App",
  components: {
    QuestionTemplate,
    Button,
  },
  data() {
    return {
      questions: [{}],
      currentQuestion: 0,
      isResultPage: false,
    };
  },
  created() {
    this.questions = [
      {
        question:
          "A car averages 27 miles per gallon. If gas costs $4.04 per gallon, which of the following is closest to how much the gas would cost for this car to travel 2,727 typical miles?",
        answers: ["$44.44", "$109.08", "$118.80", "$408.04", "$444.40"],
        selectedAnswer: "-1",
        answer: 3,
      },
      {
        question:
          "When x = 3 and y = 5, by how much does the value of 3x2 – 2y exceed the value of 2x2 – 3y ?",
        answers: ["4", "14", "16", "20", "50"],
        selectedAnswer: "-1",
        answer: 1,
      },
      {
        question: "What is the greatest common factor of 42, 126, and 210 ?",
        answers: ["2", "6", "14", "21", "42"],
        selectedAnswer: "-1",
        answer: 2,
      },
      {
        question:
          "Sales for a business were 3 million dollars more the second year than the first, and sales for the third year were double the sales for the second year. If sales for the third year were 38 million dollars, what were sales, in millions of dollars, for the first year?",
        answers: ["16", "17.5", "20.5", "22", "35"],
        selectedAnswer: "-1",
        answer: 0,
      },
      {
        question: "How many irrational numbers are there between 1 and 6 ?",
        answers: ["1", "3", "4", "10", "Infinitely many"],
        selectedAnswer: "-1",
        answer: 4,
      },
    ];
  },
  methods: {
    SetQuestionAnswer(questionIndex, index) {
      this.questions = this.questions.map((question, questionNumber) => {
        if (questionIndex == questionNumber && !this.resultPage) {
          question.selectedAnswer = index;
        }
        return question;
      });
    },
    ResetCurrentQuestion() {
      this.currentQuestion = 0;
      this.questions = this.questions.map((question) => {
        question.selectedAnswer = "-1";
        return question;
      });
      this.isResultPage = false;
    },
    IncreaseCurrentQuestion() {
      this.currentQuestion = this.currentQuestion + 1;
    },
    OpenResultPage() {
      this.isResultPage = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  margin: 0px;
  padding: 0px;
}
.mainDiv {
  background-color: cornflowerblue;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.questionArea {
  background-color: #f7c59f;
  width: 1000px;
  padding: 25px;
  border-radius: 10px;
}
.buttons {
  display: flex;
  justify-content: space-between;
  margin-left: 50px;
  margin-right: 50px;
  margin-top: 25px;
}
</style>
