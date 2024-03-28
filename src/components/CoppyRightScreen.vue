<template>
  <p class="note">
    Mẹ chơi đc thì chơi, ko chơi đc out
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
