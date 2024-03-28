<template>
  <div class="wp-main">
    <h1>Favorite soccer player</h1>
    <h4>⚽💖Highly entertaining game💖⚽</h4>
    <div class="container">
      <button @click="onMatch(16)">
        <h1>4x4</h1>
        <span>Easy</span>
      </button>
      <button @click="onMatch(36)">
        <h1>6x6</h1>
        <span>Normal</span>
      </button>
      <button @click="onMatch(64)">
        <h1>8x8</h1>
        <span>Difficult</span>
      </button>
      <button @click="onMatch(100)">
        <h1>10x10</h1>
        <span>Ex difficult</span>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onMatch(level) {
      this.$emit("onStart", { level });
    },
  },
};
</script>
<style lang="css" scoped>
.wp-main {
  color: aliceblue;
  text-align: center;
  margin-top: 110px;
}
.wp-main > h1 {
  font-size: 60px;
  margin-bottom: 20px;
}
h4 {
  margin-bottom: 49px;
}
.container h1 {
  margin: 2px 0;
}
button {
  width: 90px;
  height: 80px;
  margin: 0 8px;
  border-radius: 21px;
  padding: 5px;
  cursor: pointer;
}
button:hover {
  background-color: antiquewhite;
}
</style>
