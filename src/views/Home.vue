<template>
  <div>
    <div class="search-area">
      <div class="search-container">
        <input type="text" placeholder="Type a word" v-model="userInput">
        <img src="../assets/search.svg" alt="" class="image search" @click="dictionary">
      </div>
    </div>
    <div class="result-section">
      <div v-if="loading">Loading...</div>
      <div v-if="!success" class="error">Sorry! Word not found. Try another word or check <a href="https://www.thesaurus.com/" target="_blank"> here</a></div>
      <div v-if="!networkSuccess" class="error">Network error! Try refreshing the page</div>
      <ul v-for="(definition, index) in definitions" :key="index">
        <li>
          <div>
            <div>
              <span> {{definition.emoji}} </span>
              <span class="word"> {{word}} </span>
              <span> <img src="../assets/speaker.svg" class="image speaker" @click="speak"> </span>
              <span class="description" v-if="pronunciation !=null">({{pronunciation}})</span>
            </div>
            <p>
              <span class="description">Type: </span>
              <span> {{definition.type}} </span>
            </p>
            <p>
              <span class="description">Definition: </span>
              <span> {{definition.definition}}</span>
            </p>
            <p>
              <span class="description" v-if="definition.example !=null">Example: </span>
              <span> {{definition.example}}</span>
            </p>
            <p>
              <img :src="definition.image_url" alt="" class="word-image">
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Owlbot from 'owlbot-js'
export default {
  data () {
    return {
      definitions: '',
      userInput: '',
      pronunciation: '',
      word: '',
      loading: true,
      success: true,
      networkSuccess: true
    }
  },
  methods: {
    dictionary () {
      const client = Owlbot('1a6579739b9442d441282610641b8dc2f9edd03e')
      this.loading = true
      const vm = this
      client.define(this.userInput).then(function (result) {
        vm.loading = false
        vm.success = true
        vm.definitions = result.definitions
        vm.pronunciation = result.pronunciation
        vm.word = result.word
        vm.userInput = ''
        console.log(result)
      }).catch((error) => {
        vm.loading = false
        vm.success = false
        vm.userInput = ''
        console.log(error)
      })
    },
    speak () {
      const synth = window.speechSynthesis // instantiates the speechSynthesis API
      const speakText = new SpeechSynthesisUtterance(this.word) // passes the word into the speechSynthesis utterance
      synth.speak(speakText) // calls the speak method
    }
  },
  mounted () {
    const client = Owlbot('1a6579739b9442d441282610641b8dc2f9edd03e')
    this.loading = true
    const vm = this
    client.define('dove').then(function (result) {
      vm.loading = false
      vm.definitions = result.definitions
      vm.pronunciation = result.pronunciation
      vm.word = result.word
      vm.networkSuccess = true
      console.log(result)
    }).catch((error) => {
      vm.networkSuccess = false
      vm.loading = false
      console.log(error)
    })
  }

}
</script>
<style scoped>
  ul li {
    list-style-type: none;
  }
  .image {
    width: 25px;
    height: 25px;
  }
  .word-image {
    width: 50%;
  }
  .search-area {
    background-color: #4655A0;
    padding-bottom: 10px;
  }
  .search-container {
    width: 80%;
    display: flex;
    margin: auto;
  }
  .search-container > input {
    border-right: none;
    width: 100%;
    height: 40px;
    outline: none;
    padding-left: 10px;
    font-size: 1.6rem;
    color: #4655A0;
  }
  .search {
    margin: 7px -40px 0px;
    cursor: pointer;
  }
  .result-section {
    width: 80%;
    margin: auto;
    margin-bottom: 20px;
    color: #4655A0;
    font-size: 1.6rem;
    line-height: 2.5rem;
  }
  .word {
    font-size: 2rem;
  }
  .description {
    font-style: italic;
    font-size: 1.2rem;
  }
  .error {
    color: red;
  }
  .network-error {
    display: none;
  }
  .speaker {
    cursor: pointer;
  }
  @media (max-width: 760px) {
    .search-container {
      width: 95%;
    }
    .word-image {
      width: 100%;
   }
  }
</style>
