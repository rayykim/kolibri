<template>

  <div>
    <!-- complete -->
    <svg v-if="thisIs('complete', 'audio')" src="./content-icons/complete-audio.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('complete', 'document')" src="./content-icons/complete-document.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('complete', 'exercise')" src="./content-icons/complete-exercise.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('complete', 'video')" src="./content-icons/complete-video.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>

    <!-- partial -->
    <svg v-if="thisIs('partial', 'audio')" src="./content-icons/partial-audio.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('partial', 'document')" src="./content-icons/partial-document.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('partial', 'exercise')" src="./content-icons/partial-exercise.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('partial', 'video')" src="./content-icons/partial-video.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>

    <!-- unstarted -->
    <svg v-if="thisIs('unstarted', 'audio')" src="./content-icons/unstarted-audio.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('unstarted', 'document')" src="./content-icons/unstarted-document.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('unstarted', 'exercise')" src="./content-icons/unstarted-exercise.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
    <svg v-if="thisIs('unstarted', 'video')" src="./content-icons/unstarted-video.svg" :class="{pageicon: ispageicon}" :title="altText" :width="size" :height="size"></svg>
  </div>

</template>


<script>

  const PROGRESS_STATES = ['complete', 'partial', 'unstarted'];
  const KINDS = ['audio', 'document', 'video']; // not 'exercise' for now

  module.exports = {
    props: {
      ispageicon: {
        type: Boolean,
        default: false,
      },
      size: {
        type: Number,
        default: 30,
      },
      progress: {
        type: String,
        default: 'unstarted',
        validator(value) {
          return PROGRESS_STATES.indexOf(value) !== -1;
        },
      },
      kind: {
        type: String,
        required: true,
        validator(value) {
          return KINDS.indexOf(value) !== -1;
        },
      },
    },
    computed: {
      altText() {
        // TODO - I18N
        return `${this.progress} - ${this.kind}`;
      },
    },
    methods: {
      thisIs(progress, kind) {
        return this.progress === progress && this.kind === kind;
      },
    },
  };

</script>


<style lang="stylus" scoped>

  @require '~core-theme.styl'

  // replace the correct path
  .pageicon [fill='#996189']
    fill: $core-text-default

  .pageicon [fill='#FFF']
    fill: none

</style>
