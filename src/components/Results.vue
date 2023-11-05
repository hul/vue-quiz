<template>
  <div>
    Koniec! Twój wynik to {{ score }}!
    <button @click="onRestart">Jeszcze raz</button>
  </div>
</template>

<script>
export default {
  name: "Results",
  props: ["score", "onRestart"],
};
</script>