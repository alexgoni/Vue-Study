<template>
  <div>
    <h1>{{ result }}</h1>
    <form @submit.prevent="onSubmitForm">
      <input ref="answer" type="number" maxlength="4" v-model="value" />
    </form>
    <div>시도: {{ result }}</div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const value = ref("");
    const result = ref("");

    const onSubmitForm = (e) => {
      // e.preventDefault()는 @submit.prevent로 처리됩니다.
    };

    return {
      value,
      result,
      onSubmitForm,
    };
  },
};
</script>

<style scoped></style>
