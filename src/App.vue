<template>
  <div class="container-main">
    <h1 class="title">Simple English to English Dictionary</h1>
    <div class="flex word">
      <input
        class="word-input"
        type="text"
        name=""
        id=""
        v-model="searchWord"
        placeholder="Type Something Here!"
        @keyup.enter="fetchWord"
      />
      <button class="word-button" @click="fetchWord">Search</button>
    </div>
    <div v-if="wordInfo === null && firstSearch === true">
      <p class="show-result">Welcome To This Dictionary App</p>
      <p class="show-result">
        By Simply Enter The Word/Words You Want To Search
      </p>
      <p class="show-result">You Can Get the Result in No Time</p>
    </div>
    <p
      class="show-result"
      v-else-if="wordInfo === null && firstSearch === false"
    >
      Loading...Please wait patiently for the result...
    </p>
    <p
      class="show-result"
      v-else-if="wordInfo != null && wordInfoErr === false"
    >
      Here are the Results of the Word "<span id="the-word">{{
        wordInfo.word.toUpperCase()
      }}</span
      >"
    </p>
    <p class="show-result" v-else-if="wordInfo != null && wordInfoErr === true">
      {{ wordInfo }}
    </p>
    <div class="word-list" v-if="wordInfo != null && wordInfoErr === false">
      <div
        v-for="word in wordInfo.meanings"
        :key="wordInfo.meanings.indexOf(word)"
      >
        <word-detail
          :vocabulary="wordInfo.word"
          :meanings="
            wordInfo.meanings[wordInfo.meanings.indexOf(word)].partOfSpeech
          "
        ></word-detail>
        <word-example
          v-for="example in word.definitions"
          :key="example"
          :definition="example.definition"
          :sentence="
            example.example === undefined
              ? 'Oops! Sorry, we do not have any example yet!'
              : example.example
          "
          :noExample="example.example === undefined ? 'alert' : 'okay'"
        ></word-example>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import WordDetail from "./components/WordDetail.vue";
import WordExample from "./components/WordExample.vue";

const firstSearch = ref(true);
const wordInfoErr = ref(false);
const wordInfo = ref(null);
const searchWord = ref("");

async function fetchWord() {
  searchWord.value = searchWord.value.trim();
  if (searchWord.value === "") {
    return;
  }
  firstSearch.value = false;
  wordInfo.value = null;
  wordInfoErr.value = false;
  const res = await fetch(
    `https://api.dictionaryapi.dev/api/v2/entries/en/${searchWord.value}`
  );

  const datas = await res.json();

  if (datas.length > 0) {
    const [data] = datas;
    wordInfo.value = data;
  } else {
    wordInfoErr.value = true;
    wordInfo.value = "Can't find the word that you are looking for...";
  }
}
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
  font-size: 3.5rem;
  margin-top: 30px;
}

.word {
  justify-content: space-between;
  margin-top: 50px;

  .word-input {
    font-size: 3rem;
    width: 700px;
    background-color: rgb(219, 255, 255);
    outline: none;
  }

  .word-input:focus {
    background-color: rgb(160, 255, 255);
  }

  .word-input:focus::placeholder {
    color: transparent;
  }

  .word-button {
    font-size: 3rem;
    width: 200px;
    border-radius: 5px;
    border: 1px solid rgb(150, 150, 150);
    padding: 10px;
    background-color: rgb(227, 227, 227);
    cursor: pointer;
  }

  .word-button:hover {
    border: 1px solid rgb(106, 106, 106);
    background-color: rgb(189, 189, 189);
  }
}

.word-list {
  background-color: rgb(244, 244, 244);
  padding-bottom: 30px;
}

.flex {
  display: flex;
}

#the-word {
  font-size: 4rem;
  color: rgb(17, 0, 255);
  font-weight: 700;
}

@media (max-width: 980px) {
  .container-main {
    width: 750px;
  }

  .title {
    font-size: 4.5rem;
  }

  .word {
    justify-content: space-between;
    margin-top: 50px;

    .word-input {
      width: 600px;
    }

    .word-button {
      width: 120px;
    }
  }

  .show-result {
    font-size: 3rem;
  }
}

@media (max-width: 750px) {
  .container-main {
    width: 600px;
  }

  .title {
    font-size: 3rem;
  }

  .word {
    .word-input {
      width: 450px;
    }

    .word-button {
      width: 120px;
    }
  }
}

.show-result {
  font-size: 3rem;
}

@media (max-width: 450px) {
  .container-main {
    width: 400px;
  }

  .title {
    font-size: 2.5rem;
  }

  .word {
    .word-input {
      width: 270px;
    }

    .word-input::placeholder {
      font-size: 20px;
    }

    .word-button {
      width: 100px;
      font-size: 20px;
    }
  }
  .show-result {
    font-size: 2rem;
  }
}
</style>