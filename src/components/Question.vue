<template>
  <div>
    <h2>{{ question.question }}</h2>
    <ul>
      <li v-for="answer in question.answers" v-bind:key="answer.answer">
        <button @click="onAnswer(answer.correct)">
          {{ answer.answer }}
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Question",
  props: ["question", "onAnswer"],
};
</script>