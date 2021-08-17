<template>
<header>
 <nav>
  <h1>Improve your Typing Speed</h1>
 </nav>
</header>
</template>

<script>
export default {

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

header {
 width: 100%;
 height: 8rem;
 background: map-get($colors, "blue");
 @include flex();
 color: map-get($colors, "white");
 font-size: 2rem;
 box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;

}
</style>
