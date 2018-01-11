<template>
  <div :style="{ backgroundColor: `hsl(${x}, 80%, 50%)` }" @mousemove="xCoordinate">
    <img src="./assets/logo.png">
    <div class= "textContainer">
      {{text}} Nice to meet Vue.
    </div>
	<ul>
	  <li v-for="item in items">
		  {{ item }}
	  </li>
	</ul>
	<textarea v-model="message" class="message" rows="5" maxlength="72"></textarea><br>
	<p class="booktext">{{ message }} </p>
	  <p>
		  <button @click="increment">+</button>
		  {{ counter }}
		  <button @click="decrement">-</button>
	  </p>
	  <p>Pixels across: {{ x }}</p>
	<Helloname :rext="message" :passedNumber="x"></Helloname>
  </div>

</template>

<script>
	import Hullo from './components/HelloWorld.vue' ;

export default {
	data: function() {
		return {
			text: 'hello World inside',
			items: [
				'rung',
				'bung',
				'lung'
			],
			message: 'targeting child component',
			counter: -5,
			x: 0
		}
	},
	methods: {
		increment() {
			this.counter++;
		},
		decrement() {
			this.counter--;
		},
		xCoordinate(e) {
			this.x = e.clientX;
		}
	},
	components: {
		Helloname: Hullo
	}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
