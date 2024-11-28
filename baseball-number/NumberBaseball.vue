<template>
  <div>
    <form @submit.prevent="onSubmitForm">
      <input ref="answer" minlength="4" maxlength="4" v-model="value" />
      <button type="submit">입력</button>
    </form>
    <div>시도: {{ tries.length }}</div>
    <ul>
      <li v-for="(t, index) in tries" :key="index">
        <div>{{ t.try }}</div>
        <div>{{ t.result }}</div>
      </li>
    </ul>
  </div>
</template>

<script>
const getNumbers = () => {
  const candidates = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  const array = [];

  for (let i = 0; i < 4; i++) {
    const chosenIdx = Math.ceil(Math.random() * 9) - 1;
    array.push(candidates[chosenIdx]);
  }

  return array;
};

export default {
  data() {
    return {
      answer: getNumbers(),
      tries: [],
      value: "",
      result: "",
    };
  },
  methods: {
    onSubmitForm() {
      let strike = 0;
      let ball = 0;
      const valueArr = [...this.value].map((each) => Number(each));

      const compareValueAndAnswer = () => {
        for (let i = 0; i < 4; i++) {
          if (this.answer[i] === valueArr[i]) strike++;
          else if (this.answer.includes(valueArr[i])) ball++;
        }

        if (strike === 4) this.result = "홈런";
        else this.result = `${strike}스트라이크 ${ball}볼`;
        this.tries.push({
          try: this.value,
          result: this.result,
        });
      };

      const resetGame = () => {
        const confirm = window.confirm("게임을 다시 시작할까요?");
        if (confirm) {
          this.tries = [];
          this.answer = getNumbers();
          this.result = "";
        }
      };

      compareValueAndAnswer();
      if (this.result === "홈런") resetGame();
      else if (this.tries.length >= 10) {
        alert(`정답은 ${this.answer.join("")} 입니다!`);
        resetGame();
      }

      this.value = "";
      this.$refs.answer.focus();
    },
  },
};
</script>

<style></style>
