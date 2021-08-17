<template>
<div class="score">
 <h3>Time is over</h3>
 <p>{{chooseAnswer}} WPM <small>(words per minute)</small> </p>
 <span>Accuracy Percentage : %{{truePercent}} </span><br>
 <span>Correct word : {{trueCount}} </span><br>
 <span>Wrong word: {{falseCount}} </span>
</div>
</template>

<script>
export default {
 props: ["trueCount", "falseCount", "chooseAnswer"],
 data() {
 },
 computed: {
  truePercent() {
   return  ((100 / this.chooseAnswer) * this.trueCount).toFixed(2);
  }
 },
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

@mixin flex() {
 display: flex;
 align-items: center;
 justify-content: center;
}

.score {
 background: map-get($colors, "white");
 box-shadow: rgba(0, 0, 0, 0.4) 0px 2px 4px, rgba(0, 0, 0, 0.3) 0px 7px 13px -3px, rgba(0, 0, 0, 0.2) 0px -3px 0px inset;
 padding: 3rem;
 width: 36rem;
 height: 35rem;
 line-height: 4rem;
 border-radius: 2rem;

 h3 {
  font-size: 3rem;
  text-shadow: .3rem 1rem 2rem map-get($colors, "black");
  @include flex();
  margin-bottom: 2rem;
 }

 >* {
  font-size: 1.7rem;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  color: map-get($colors, "green");
 }

 small {
  color: map-get($colors, "black");
  font-size: 1.3rem;
  display: block;
  position: relative;
  top: -1rem;
 }
}
</style>
