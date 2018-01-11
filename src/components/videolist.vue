<template>
  <div class="video-list media" @click="newVideoID">
    <div class="media-left">
    <img :src="thumbnail" />
  </div>
    <div class="media-left media-description">{{description}}</div>
  </div>
</template>

<script>
  export default {
    props: {
      thumbnail: {
        type: String,
        required: true
      },
      description: {
        type: String,
        required: true
      },
      videoID: {
        type: String
      }
    },
    methods: {
      newVideoID: function () {
        this.$emit('passupid', this.videoID)
      }
    }
  }
</script>

<style lang="scss">

</style>
