<template>
  <div class="word-example">
    <p class="word-example__definition">
      <span>Definintion:</span>
      <span>{{ props.definition }}</span>
    </p>
    <p class="word-example__sentence">
      <span>Example:</span>
      <span :class="noExample">{{ props.sentence }}</span>
    </p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  definition: String,
  sentence: String,
  noExample: String,
});
</script>

<style lang='scss' scoped>
.word-example {
  margin-top: 20px;

  &__definition {
    display: flex;
    gap: 15px;
    margin-top: 30px;
    font-size: 3rem;
    margin-bottom: 10px;
    color: rgb(102, 58, 0);
    span {
      font-size: 3rem;
    }
  }

  &__sentence {
    display: flex;
    gap: 47px;
    margin-top: 30px;
    font-size: 2.8rem;
    color: rgb(0, 0, 0);
    span {
      font-size: 3rem;
    }
  }
}

.alert {
  color: rgb(255, 0, 0);
}

.okay {
}
</style>