<template>
  <div id="app">
    Vue.js component test
    <searchbar-c v-on:passupstring="queryapi"></searchbar-c>
    <span>{{searchquery}}</span>
    <div class="content-holder">
      <VideodetailsC v-bind:activeVideoIDC="activeVideoID" v-if="responseIn"></VideodetailsC>
      <ul class="videolist" v-if="responseIn">
        <li v-for="video  in testVideos">
          <VideoListC v-bind:thumbnail="video.image" v-bind:description="video.title" v-bind:videoID="video.videoID" v-on:passupid="changeVideo"></VideoListC>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  import Videolist from './components/videolist.vue'
  import Videodetails from './components/videodetails.vue'
  import Searchbar from './components/searchbar.vue'

export default {
  data: function () {
    return {
      searchquery: '',
      json: null,
      activeVideoObject: null,
      activeVideoID: '',
      responseIn: false,
      testVideos: null,
      toplevelprop: 1
    }
  },
  methods: {
    changeVideo (incomingID) {
      this.activeVideoID = 'https://www.youtube.com/embed/' + incomingID
    },
    queryapi (incomingString) {
      let url = 'https://www.googleapis.com/youtube/v3/search?part=snippet&q=' + incomingString + '&key=AIzaSyC_U2Wqv8eJcSWAq5nWZdW80OfOmlKh27Y'
      fetch(url)
        .then(r => r.json())
        .then(json => {
          this.json = json
          this.activeVideoObject = json.items[0]
          this.activeVideoID = 'https://www.youtube.com/embed/' + this.activeVideoObject.id.videoId
          this.testVideos = json.items.map((video) => {
            return (
              {title: video.snippet.title, image: video.snippet.thumbnails.medium.url, videoID: video.id.videoId}
            )
          })
          this.responseIn = true
        })
    }
  },
  components: {
    VideoListC: Videolist,
    VideodetailsC: Videodetails,
    SearchbarC: Searchbar
  }
}
</script>

<style lang="scss">
/*
install scss requirements before running
npm install sass-loader node-sass --save-dev
*/
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin:60px auto 0;
  width: 800px;
}
input {
	width: 300px;
	padding: 3px;
}
.video-list {
  cursor: pointer;
  border-bottom: 1px solid black;
  height: 200px;
  clear: both;
  margin-bottom: 20px;

.media-description {
  text-align: left;
  width: 50%;
  padding-left: 10px;
}

.media-left {
  float: left;
}
}
  ul {
    list-style: none;
  }
</style>
