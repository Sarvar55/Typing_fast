<template>
<Nav></Nav>
<div class="container">
 <Score  v-if="show"  :trueCount="trueCount" :falseCount="falseCount"  :chooseAnswer="chooseAnswer" />
 <div class="wrapper" v-else>
  <div class="text__area">
   <span v-for="(word, key) in words.filter((data,index)=>index < 15)" :key="key" :class="key==0 &&  classControl">{{ word  }}</span>
  </div>
  <div class="bottom">
   <input type="text" class="text" v-model="text" @input="textControl($event)">
   <button class="btn">{{timer}} sn. </button>
   <button :disabled="isRuning" class="btn" @click="getWords">Reset</button>
  </div>
 </div>
</div>
</template>

<script>
import wordList from '@/assets/words.json';

import Score from '@/components/Score.vue';
import Nav from '@/components/Nav';

export default {
 components: {
  Score,
  Nav,
 },
 data() {
  return {
   wordList: wordList,
   text: null,
   words: [],
   isTrue: true,
   trueCount: 0,
   falseCount: 0,
   timer: 60,
   interval: false,
   isRuning: false,
   show: false,
  }
 },
 mounted() {
  this.getWords();
 },
 methods: {
  getWords() {
   this.words = this.wordList.sort(() => Math.random() - 0.5).splice(0, 300);
  },
  toogleTimer() {
   this.isRuning = true;
   this.interval = setInterval(() => {
    if (this.timer == 0) {
     this.show = true;
     clearInterval(this.interval);
     return;
    }
    this.timer--;
   }, 1000)
  },
  textControl(event) {
   console.log(event.target.value.length)
   return event.target.value.length == 0 ? false : true;
  }
 },
 computed: {
  classControl() {
   return this.isTrue ? 'correct' : 'incorrect';
  },
  chooseAnswer() {
   return 300 - this.words.length;
  },
 },
 watch: {
  text(val) {
   if (!this.isRuning) this.toogleTimer();
   const word = this.words[0].slice(0, val.length); // mes  word w o r d 
   const userWord = val.replace(" ", "");
   
   this.isTrue = word === userWord; // true or false

   if (val.indexOf(" ") !== -1) {
    this.isTrue ? ++this.trueCount : ++this.falseCount;
    this.words.splice(0, 1);
    this.text = "";
    this.isTrue = true;
   }
  }
 }
}
</script>

<style lang="scss">
$colors:("blue":#1e3799,
 "red":#eb2f06,
 "black":#353b48,
 "green":#4cd137,
 "porple":#8c7ae6,
 "light":#00a8ff,
 "white": #f5f6fa,
 "black1":#95afc0,
);

*::before,
*::after,
* {
 margin: 0;
 padding: 0;
 box-sizing: border-box;
}

html {
 font-size: 62.5%;
}

body {
 background: map-get($colors, "black");
}

@mixin flex() {
 display: flex;
 align-items: center;
 justify-content: center;
}

.container {
 @include flex();
 width: 100%;
 height: 100vh;

 .wrapper {
  width: 60rem;
  background: map-get($colors, "light");
  border-radius: 1rem;
  @include flex();
  flex-direction: column;
  height: 40rem;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;

  .text__area {
   width: 48rem;
   border-radius: 1rem;
   margin-bottom: 3rem;
   box-shadow: rgba(29, 29, 37, 0.25) 0px 30px 60px -2px inset, rgba(251, 251, 251, 0.3) 0px 18px 36px -1px inset;
   height: 15rem;
   background: map-get($colors, "white");
   padding: 1.4rem;
   overflow: hidden;

   span {
    font-size: 1.9rem;
    margin: 0 .7rem;
    font-weight: 400;
    display: inline-block;
    line-height: 3rem;
   }
  }

  .bottom {
   background: rgba(255, 255, 255, 0.4);
   width: 100%;
   height: 10rem;
   @include flex();
   margin: 3rem 0 0 0;

   .text {
    padding: 2rem;
    font-size: 2rem;
    color: map-get($colors, "white");
    width: 30rem;
    border: 0;
    outline: 0;
    background: transparent;
    border-block-end: 2px solid map-get($colors, "porple");
    margin: 0 2rem;
   }

   .btn {
    padding: 1rem;
    position: relative;
    top: 1rem;
    background: map-get($colors, "black");
    width: 8rem;
    margin: 0 .5rem;
    border-radius: 1rem;
    border: 0;
    outline: 0;
    cursor: pointer;
    box-shadow: rgba(14, 30, 37, 0.12) 0px 2px 4px 0px, rgba(14, 30, 37, 0.32) 0px 2px 16px 0px;
    color: map-get($colors, "white");
    font-size: 1.6rem;
    font-weight: 500;
   }
  }
 }
}

.correct {
 background: map-get($colors, "green");
 border-radius: .8rem;
 padding: .5rem;
}

.incorrect {
 background: map-get($colors, "red");
 border-radius: .8rem;
 padding: .5rem;
}
</style>
