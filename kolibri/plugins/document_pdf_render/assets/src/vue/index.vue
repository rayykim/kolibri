<template>

  <div>
    <div v-el:container class="container" allowfullscreen>
      <button class='btn' v-if="supportsPDFs" v-on:click="togglefullscreen">Toggle Fullscreen</button>
      <div v-el:pdfcontainer class="pdfcontainer"></div>
    </div>
  </div>

</template>


<script>

  const PDFobject = require('pdfobject');

  module.exports = {

    props: ['defaultFile'],

    data: () => ({
      supportsPDFs: PDFobject.supportsPDFs,
    }),

    methods: {
      togglefullscreen() {
        const container = this.$els.container;
        if (!document.fullscreenElement
          && !document.webkitFullscreenElement
          && !document.mozFullScreenElement
          && !document.msFullscreenElement) {
          if (container.requestFullscreen) {
            container.requestFullscreen();
          } else if (container.webkitRequestFullscreen) {
            container.webkitRequestFullscreen();
          } else if (container.mozRequestFullScreen) {
            container.mozRequestFullScreen();
          } else if (container.msRequestFullscreen) {
            container.msRequestFullscreen();
          }
        } else {
          if (document.exitFullscreen) {
            document.exitFullscreen();
          } else if (document.webkitExitFullscreen) {
            document.webkitExitFullscreen();
          } else if (document.mozCancelFullScreen) {
            document.mozCancelFullScreen();
          } else if (document.msExitFullscreen) {
            document.msExitFullscreen();
          }
        }
      },
    },

    ready() {
      PDFobject.embed(this.defaultFile.storage_url, this.$els.pdfcontainer);
    },

  };

</script>


<style lang="stylus" scoped>

  .btn
    margin-bottom: 1em

  .container
    text-align: center
    height: 100%
    &:fullscreen
      width: 100%
      height: 100%

  .pdfcontainer
    /* Accounts for the button height. */
    height: calc(100% - 4em)

</style>
