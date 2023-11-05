<template>
  <div>
    <span>Pytanie {{ current + 1 }} z {{ count }}</span>
    <button v-bind:disabled="isFirst" @click="onPrevious">Poprzednie</button>
    <button v-bind:disabled="isLast" @click="onNext">Następne</button>
  </div>
</template>

<script>
export default {
  name: "Navigation",
  props: ["current", "count", "isFirst", "isLast", "onPrevious", "onNext"],
};
</script>