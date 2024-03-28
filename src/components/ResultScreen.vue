<template>
  <div id="result">
    <h1>🌟💖🌟 You have completed 🌟💖🌟</h1>
    <p>
      In {{ Math.round(timer / 1000) }} seconds
    </p>

    <button @click="onStartAgain()">Start Again</button>
  </div>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
<style scoped>
#result {
  text-align: center;
  margin-top: 150px;
  margin-bottom: 87px;
}
h1 {
  color: aliceblue;
  font-size: 41px;
}
p {
  color: aliceblue;
  margin-bottom: 40px;
}
button {
  padding: 10px 5px;
  border-radius: 7px;
  cursor: pointer;
}
button:hover {
  background: #ddc6c6;
}
</style>
