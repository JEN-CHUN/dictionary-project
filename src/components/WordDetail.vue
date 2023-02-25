<template>
  <div class="word-list">
    <div class="word-info">
      <p class="word-info__vocabulary">{{ props.vocabulary }}</p>
      <p class="word-info__part-of-speech">{{ props.noun }}</p>
      <p class="word-info__phonetic">{{ props.phonetic }}</p>
    </div>
    <div class="word-example">
      <p class="word-example__definition">{{ props.definition }}</p>
      <p class="word-example__sentence">{{ props.sentence }}</p>
    </div>
  </div>
</template>

<script setup>

import { defineProps } from "vue";

const props = defineProps({
  vocabulary: String,
  noun: String,
  phonetic: String,
  definition: String,
  sentence: String,
})

</script>

<style lang='scss' scoped>
.word-list {
  background-color: blanchedalmond;
}

.word-info {
  display: flex;
  align-items: flex-end;
  gap: 30px;
  margin-top: 20px;

  &__vocabulary {
    font-size: 3rem;
  }

  &__phonetic {
    font-size: 2.5rem;
  }

  &__part-of-speech {
    font-size: 2.5rem;
  }

}

.word-example {
  margin-top: 20px;

  &__definition {
    font-size: 2.5rem;
    margin-bottom: 10px;
  }

  &__sentence {
    font-size: 2.5rem;
  }
}
</style>