<template>
  <div>
    <div v-if="!isCompleted">
      <Navigation
        v-bind:current="current"
        v-bind:count="questionsCount"
        v-bind:isFirst="isFirstQuestion"
        v-bind:isLast="isLastQuestion"
        v-bind:onPrevious="previousQuestion"
        v-bind:onNext="nextQuestion"
      />
      <Question v-bind:question="question" v-bind:onAnswer="onAnswer" />
      <Score v-bind:score="points" />
    </div>
    <div v-if="isCompleted">
      <Results v-bind:score="points" v-bind:onRestart="restart" />
    </div>
  </div>
</template>

<script>
import Navigation from "./Navigation";
import Question from "./Question";
import Score from "./Score";
import Results from "./Results";

const questions = [
  {
    question:
      "Jaki napis widniał na torcie, który Hagrid podarował Harry’emu z okazji 11. urodzin?",
    answers: [
      { answer: "11 Urodziny Harrego", correct: false },
      { answer: "Wszystkiego najlepszego Harry", correct: false },
      { answer: "Harry'emu w dniu urodzin", correct: true },
    ],
  },
  {
    question: "Skąd Lily wiedziała o korespondencji Petunii z Dumbledorem?",
    answers: [
      { answer: "Petunia jej o tym powiedziała", correct: false },
      { answer: "Lilly znalazła list Petunii", correct: false },
      { answer: "Snape znalazł jej list", correct: true },
    ],
  },
  {
    question: "Dokąd Harry i Cho wybrali się na Walentynki?",
    answers: [
      { answer: "Do herbaciarni", correct: true },
      { answer: "Do Trzech Mioteł", correct: false },
      { answer: "Do Dziurawego Kotła", correct: true },
    ],
  },
  {
    question:
      "Gdzie śmierciożercy zwykli handlować swoimi wywarami i truciznami?",
    answers: [
      { answer: "W zaułkach ulicy Śmiertelnego Nokturnu", correct: true },
      { answer: "W sklepie Borkina i Burkesa", correct: false },
      { answer: "W Gospodzie pod Świńskim Łbem", correct: true },
    ],
  },
];

export default {
  name: "Quiz",
  components: { Navigation, Question, Score, Results },
  data() {
    return {
      current: 0,
      points: 0,
      questions,
      isCompleted: false,
    };
  },
  computed: {
    question() {
      return this.questions[this.current];
    },
    isFirstQuestion() {
      return this.current === 0;
    },
    isLastQuestion() {
      return this.current === this.questions.length - 1;
    },
    questionsCount() {
      return this.questions.length;
    },
  },
  methods: {
    nextQuestion() {
      if (!this.isLastQuestion) {
        this.current++;
      } else {
        this.isCompleted = true;
      }
    },
    previousQuestion() {
      this.current--;
    },
    onAnswer(correct) {
      if (correct) {
        this.answerCorrect();
      } else {
        this.answerWrong();
      }
      this.onNextQuestion();
    },
    answerCorrect() {
      this.points++;
    },
    answerWrong() {
      if (this.points > 0) this.points--;
    },
    restart() {
      this.current = 0;
      this.question = 0;
      this.points = 0;
      this.isCompleted = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
pre {
  text-align: "left";
}
</style>
