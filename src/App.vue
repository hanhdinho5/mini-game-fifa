<template>
  <main-screen
    v-if="status === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="status === 'match'"
    :cardcontext="settings.cardcontext"
    @onfinishGame="finishGame"
  />
  <result-screen
    v-if="status === 'finish'"
    :timer="timer"
    @onStartAgain="swithScreenDefault()"
  />
  <coppy-right-screen
    v-if="status !== 'default' && status !== 'finish'"
    @onStartAgain="swithScreenDefault()"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utilities/array";
import ResultScreen from "./components/ResultScreen.vue";
import CoppyRightScreen from "./components/CoppyRightScreen.vue";

export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CoppyRightScreen,
  },
  data() {
    return {
      status: "default",
      settings: {
        totalOfBlock: 0,
        cardcontext: [],
        time: null,
      },
      timer: 0,
    };
  },
  methods: {
    onHandleBeforeStart(data) {
      // console.log("ok", data);
      this.settings.totalOfBlock = data.level;
      // console.log(this.settings.totalOfBlock);
      const firstCards = Array.from(
        { length: this.settings.totalOfBlock / 2 }, // Số phần tử mảng
        (_, i) => i + 1 // _ là biểu thị giá trị đầu vào (ko quan tâm), i là chỉ số của mỗi pt trong new array, giá trị của pt sẽ là i+1
      );
      const secondCards = [...firstCards]; // copy array sang array mới
      const Cards = [...firstCards, ...secondCards];
      this.settings.cardcontext = shuffled(shuffled(shuffled(Cards))); // Trộn 3 lần
      this.settings.time = new Date().getTime(); // gắn cho  thời gian bắt đầu, là 1 số đc tính bằng mili giây kể từ 1/1/1970
      // data ready
      this.status = "match";
    },
    finishGame() {
      // set timer
      this.timer = new Date().getTime() - this.settings.time; // lấy t hiện tại - t bắt đầu
      // screen switch
      this.status = "finish";
    },
    swithScreenDefault() {
      this.status = "default";
    },
  },
};
</script>
