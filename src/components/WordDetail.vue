<template>
  <div class="word-info">
    <p class="word-info__vocabulary">{{ props.vocabulary }}</p>
    <p class="word-info__part-of-speech">{{ props.meanings }}</p>
    <!-- <p class="word-info__phonetic">{{ props.phonetic }}</p> -->
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  vocabulary: String,
  meanings: String,
  // phonetic: String,
});
</script>

<style lang='scss' scoped>
.word-info {
  display: flex;
  align-items: flex-end;
  gap: 30px;
  margin-top: 20px;

  &__vocabulary {
    font-size: 5rem;
    color: rgb(49, 30, 255);
  }

  &__part-of-speech {
    font-size: 4rem;
    color: rgb(255, 76, 70);
  }

  &__phonetic {
    font-size: 4rem;
    color: rgb(255, 76, 70);
  }
}
</style>