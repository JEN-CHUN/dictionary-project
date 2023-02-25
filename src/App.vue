<template>
  <div class="container-main">
    <h1 class="title">Simple English to English Dictionary</h1>
    <div class="flex word">
      <input class="word-input" type="text" name="" id="" />
      <button class="word-button">Search</button>
    </div>

    <p class="show-result" v-if="wordInfo === null">
      Loading...Please wait patiently for the result...
    </p>
    <p class="show-result" v-else-if="wordInfo != null && wordInfoErr === false">
      Here are the Results of the Word "{{ wordInfo.word }}"
    </p>
    <p class="show-result" v-else-if="wordInfo != null && wordInfoErr === true">
      {{ wordInfo }}
    </p>
    <word-detail></word-detail>
  </div>
</template>

<script setup>
import { ref } from "vue";
import WordDetail from "./components/WordDetail.vue";

const wordInfoErr = ref(false);
const wordInfo = ref(null);

async function fetchWord() {
  wordInfo.value = null;
  const res = await fetch(
    "https://api.dictionaryapi.dev/api/v2/entries/en/looking"
  )

  const datas = await res.json();

  if (datas.length > 0) {
    const [data] = datas;
    wordInfo.value = data;
    console.log(wordInfo.value.word);
  } else {
    wordInfoErr.value = true;
    wordInfo.value = "Can't find the word that you are looking for...";
  }
}

fetchWord();
</script>

<style lang='scss'>
* {
  padding: 0;
  margin: 0;
  font-size: 10px;
  box-sizing: border-box;
}

.container-main {
  width: 980px;
  margin: auto;
}

.title {
  text-align: center;
  font-size: 5em;
  margin-top: 40px;
}

.show-result {
  text-align: center;
  font-size: 4rem;
  margin-top: 30px;
}

.word {
  justify-content: space-between;
  margin-top: 50px;

  .word-input {
    font-size: 3rem;
    width: 700px;
    outline: none;
  }

  .word-button {
    font-size: 3rem;
    width: 200px;
  }
}

.flex {
  display: flex;
}
</style>
