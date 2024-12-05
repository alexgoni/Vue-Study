<template>
  <div>
    <div id="computer">컴퓨터: {{ computer }}</div>
    <div id="user">나: {{ user }}</div>
    <div>
      <button @click="onClickButton('바위')">바위</button>
      <button @click="onClickButton('가위')">가위</button>
      <button @click="onClickButton('보')">보</button>
    </div>
    <div>{{ result }}</div>
    <div>현재 {{ score }}점</div>
  </div>
</template>

<script>
let intervalId;
const ROCK_SCISSOR_PAPER = ["바위", "가위", "보"];
const scores = {
  가위: 1,
  바위: 0,
  보: -1,
};

export default {
  data() {
    return {
      computer: "바위",
      user: "",
      result: "",
      score: 0,
    };
  },
  methods: {
    changeHand() {
      intervalId = setInterval(() => {
        this.computer = ROCK_SCISSOR_PAPER[Math.floor(Math.random() * 3)];
      }, 50);
    },
    onClickButton(choice) {
      clearInterval(intervalId);
      this.user = choice;

      const diff = scores[this.user] - scores[this.computer];
      if (diff === 0) this.result = "무승부";
      else if ([-1, 2].includes(diff)) {
        this.result = "승리";
        this.score++;
      } else {
        this.result = "패배";
        this.score--;
      }

      setTimeout(() => {
        this.changeHand();
      }, 2000);
    },
  },
  mounted() {
    this.changeHand();
  },
  beforeDestroy() {
    clearInterval(intervalId);
  },
};
</script>

<style scoped></style>
