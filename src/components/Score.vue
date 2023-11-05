<template>
  <div>Punkty: {{ score }}</div>
</template>

<script>
export default {
  name: "Points",
  props: ["score"],
};
</script>