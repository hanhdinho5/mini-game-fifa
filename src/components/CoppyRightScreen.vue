<template>
  <p class="note">
    Entertainment game, come back here
    <a href="#" @click="onStartAgain()">Click me</a>
  </p>
</template>
<script>
export default {
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
<style lang="css" scoped>
.note {
  color: aliceblue;
  text-align: right;
}
a {
  color: #3910ed;
}
</style>
