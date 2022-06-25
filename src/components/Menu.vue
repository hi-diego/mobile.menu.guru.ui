<template lang="pug">
v-container(class="main-menu")
  .menu-item
    v-row
      v-img.index(src="/img/products/plating.gif")
    .title.d-flex.flex-column.pa-5
      p.font-weight-light.invert--text.mb-0 Postres
      h1.text-h3.font-weight-light.invert--text() Macarroni Spligatto
      .icons.d-flex.my-5
        small.mr-10.d-flex
          v-icon.invert--text mdi-clock-outline
          span.mx-1.invert--text 30 min
        small.mr-10.d-flex
          v-icon.invert--text mdi-heart
          span.mx-1.invert--text 30
  .menu-item
    v-row
      v-img.index(src="/img/products/plating.gif")
    .title.d-flex.flex-column.pa-5
      p.font-weight-light.invert--text.mb-0 Postres
      h1.text-h3.font-weight-light.invert--text() Macarroni Spligatto
      .icons.d-flex.my-5
        small.mr-10.d-flex
          v-icon.invert--text mdi-clock-outline
          span.mx-1.invert--text 30 min
        small.mr-10.d-flex
          v-icon.invert--text mdi-heart
          span.mx-1.invert--text 30
</template>

<style>
.index {
  z-index: 5;
}
.main-menu {
  min-height: 100%;
  /*background: rgb(18,18,18);*/
  /*background: linear-gradient(7deg, rgba(18,18,18,1) 0%, rgba(63,46,46,1) 35%, rgba(38,45,73,1) 100%);*/
}
.menu-item {
  height: 100vh;
  position: relative;
  content: '';
}

.menu-item::after {
  height: 100vh;
  width: 100vw;
  content: '';
  position: absolute;
  top: 0%;
  display: flex;
  background-image: url(/img/products/plating.gif);
  background-repeat: round;
  filter: blur(37px);
}

.title {
  z-index: 5;
  position: absolute;
  top: 0px;
}
.invert--text {
  filter: invert(1) grayscale(1);
  mix-blend-mode: difference;
}
</style>

<script>
export default {
  //
  data: function () {
    return {
      publicPath: process.env.BASE_URL
    }
  }
}
/* eslint-disable */
function getAverageRGB(imgEl) {
    var blockSize = 5, // only visit every 5 pixels
        defaultRGB = {r:0,g:0,b:0}, // for non-supporting envs
        canvas = document.createElement('canvas'),
        context = canvas.getContext && canvas.getContext('2d'),
        data, width, height,
        i = -4,
        length,
        rgb = {r:0,g:0,b:0},
        count = 0;
    if (!context) {
        return defaultRGB;
    }
    height = canvas.height = imgEl.naturalHeight || imgEl.offsetHeight || imgEl.height;
    width = canvas.width = imgEl.naturalWidth || imgEl.offsetWidth || imgEl.width;
    context.drawImage(imgEl, 0, 0);
    try {
        data = context.getImageData(0, 0, width, height);
    } catch(e) {
        /* security error, img on diff domain */
        return defaultRGB;
    }
    length = data.data.length;
    while ( (i += blockSize * 4) < length ) {
        ++count;
        rgb.r += data.data[i];
        rgb.g += data.data[i+1];
        rgb.b += data.data[i+2];
    }
    // ~~ used to floor values
    rgb.r = ~~(rgb.r/count);
    rgb.g = ~~(rgb.g/count);
    rgb.b = ~~(rgb.b/count);

    return rgb;

}
</script>
