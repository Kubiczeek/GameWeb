<template>
  <div class="container">
    <p>{{ question }}</p>
    <div class="answers">
      <button
        v-for="(answer, index) in answers"
        @click="checkAnswer(answer)"
        :class="{
          correct:
            (answer === correctAnswer && selectedAnswer == answer) ||
            (selectedAnswer !== '' && answer === correctAnswer),
          wrong: answer !== correctAnswer && selectedAnswer == answer,
          unselected: selectedAnswer === '',
        }"
      >
        {{ answer }}
      </button>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "games",
});

const { data } = await useFetch("https://opentdb.com/api.php?amount=50").catch(
  (err) => {
    console.log(err);
  }
);
let currentQuestion = 0;
let question = data.value.results[currentQuestion].question;
let correctAnswer = data.value.results[currentQuestion].correct_answer;
let incorrectAnswers = data.value.results[currentQuestion].incorrect_answers;
const answers = ref(
  [correctAnswer, ...incorrectAnswers].sort(() => Math.random() - 0.5)
);

console.log(correctAnswer);

let selectedAnswer = ref("");

const checkAnswer = async (answer) => {
  if (selectedAnswer.value === "") {
    selectedAnswer.value = answer;
    if (currentQuestion >= 50) {
      console.log("first");
      await new Promise((resolve) => setTimeout(resolve, 2000));
      question =
        "No more questions for now! You can play again later. Redirecting to home page...";
      answers.value = [];
      await new Promise((resolve) => setTimeout(resolve, 2000));
      await navigateTo("/");
      return;
    }
    // Wait for 5 seconds after an answer is selected
    await new Promise((resolve) => setTimeout(resolve, 2000));
    currentQuestion += 1;
    question = data.value.results[currentQuestion].question;
    correctAnswer = data.value.results[currentQuestion].correct_answer;
    incorrectAnswers = data.value.results[currentQuestion].incorrect_answers;
    answers.value = [correctAnswer, ...incorrectAnswers].sort(
      () => Math.random() - 0.5
    );
    selectedAnswer.value = "";
  }
};
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
  background-color: $green;
  border: 3px solid $green;
  color: $white;
}

.wrong {
  background-color: $red;
  border: 3px solid $red;
  color: $white;
}
button {
  display: inline;
  font-size: 2rem;
  color: $default;
  width: 50%;
  font-weight: 400;
  border: 3px solid $default;
  border-radius: 6px;
  background-color: $main_black;
  text-align: center;
  transition: all 0.2s ease-in-out;

  &:hover {
    cursor: pointer;
  }
}

.unselected:hover {
  border: 3px solid $hover;
  color: $hover;
}
</style>
