<template>
	<div id="app">
		Vue.js component test -live
		<searchbar-component v-on:passupstring="queryapi"></searchbar-component>
		<div class="diagnostic-holder">
			<div>{{searchquery}}</div>
			<div>{{activeVideoID}}</div>
		</div>
		<div class="content-holder">
			<videodetails-component v-bind:activeVideoIDC="activeVideoID" v-if="responseIn"></videodetails-component>
			<ul class="videolist" v-if="responseIn">
				<li v-for="video  in videoArray">
					<videolist-component v-bind:thumbnail="video.image" v-bind:description="video.title" v-bind:videoID="video.videoID" v-on:passupid="changeVideo"></videolist-component>
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
		data: function() {
			return {
				searchquery: '',
				json: null,
				activeVideoObject: null,
				activeVideoID: '',
				responseIn: false,
				videoArray: null
			}
		},
		methods: {
			changeVideo (incomingID) {
				this.activeVideoID = 'https://www.youtube.com/embed/' + incomingID
			},
			queryapi (incomingString) {
				this.searchquery = incomingString
				let url = 'https://www.googleapis.com/youtube/v3/search?part=snippet&q=' + incomingString + '&key=AIzaSyC_U2Wqv8eJcSWAq5nWZdW80OfOmlKh27Y'
				fetch(url)
					.then(r => r.json())
					.then(json => {
						this.json = json
						this.activeVideoObject = json.items[0]
						this.activeVideoID = 'https://www.youtube.com/embed/' + this.activeVideoObject.id.videoId
						this.videoArray = json.items.map((video) => {
							return (
								{title: video.snippet.title, image: video.snippet.thumbnails.medium.url, videoID: video.id.videoId}
							)
						})
						this.responseIn = true
					})
			}
		},
		components: {
			VideolistComponent: Videolist,
			VideodetailsComponent: Videodetails,
			SearchbarComponent: Searchbar
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
		text-align: center;
		color: #2c3e50;
		margin: 60px auto 0;
		width: 800px;
	}

	.diagnostic-holder {
		display:none;
	}

	.videoarea {

	}

	.content-holder {

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
