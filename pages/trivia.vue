<template>
  <div class="container">
    <p>{{ question }}</p>
    <div class="answers">
      <Question-answer
        @click="checkAnswer(answer)"
        v-for="answer in answers"
        :class="{
          correct: answer === correctAnswer && answerClicked,
          wrong:
            answer === selectedAnswer &&
            answer !== correctAnswer &&
            answerClicked,
        }"
        >{{ answer }}</Question-answer
      >
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "games",
});

const { data } = await useFetch("https://opentdb.com/api.php?amount=1");
const question = data.value.results[0].question;
const correctAnswer = data.value.results[0].correct_answer;
const incorrectAnswers = data.value.results[0].incorrect_answers;
const answers = [correctAnswer, ...incorrectAnswers].sort(
  () => Math.random() - 0.5
);
console.log(correctAnswer);

let selectedAnswer = null;
let answerClicked = false;

function checkAnswer(answer) {
  selectedAnswer = answer;
  answerClicked = true;
}
</script>

<style lang="scss" scoped>
.container {
  padding-top: 5%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  gap: 100px;
}

p {
  font-size: 2rem;
  font-weight: 700;
  width: 50%;
  text-align: center;
  color: $white;
}

.answers {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 10px;
  width: 100%;
}

.correct {
  color: green;
}

.wrong {
  color: red;
}
</style>
