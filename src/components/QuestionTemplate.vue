<template>
  <div>
    <h3 class="question">{{ question.question }}</h3>
    <ul>
      <li
        v-for="(answer, index) in question.answers"
        :key="index + '-answer'"
        :id="index"
        :class="
          question.answer === question.selectedAnswer &&
          question.selectedAnswer === index &&
          isResultPage
            ? 'resultTrue'
            : isResultPage && question.selectedAnswer === index
            ? 'resultFalse'
            : ''
        "
      >
        <input
          type="checkbox"
          :disabled="isResultPage"
          :checked="question.selectedAnswer == index"
          @click="$emit('selected-answer', questionIndex, index)"
        />
        {{ answer }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "QuestionTemplate",
  props: {
    question: Object,
    questionIndex: Number,
    isResultPage: Boolean,
  },
};
</script>

<style scoped>
.question {
  text-align: left;
  margin-left: 10px;
}

ul {
  list-style-type: none;
  text-align: left;
}

li {
  margin-top: 20px;
}

.resultTrue {
  background-color: #00c49a;
}

.resultFalse {
  background-color: #ff0000;
}
</style>
