<template>
  <div class="videoarea">
    <input class="submit-field"
      autofocus autocomplete="off"
      placeholder="Enter search term?"
      v-model="searchValue"
      @keyup.enter="broadcastsearchstring">
    </input>
    <button v-on:click="broadcastsearchstring">Search</button>
  </div>
</template>
<script>
  export default {
    data: function () {
      return {
        searchValue: ''
      }
    },
    methods: {
      broadcastsearchstring: function () {
        this.$emit('passupstring', this.searchValue)
      }
    }
  }
</script>
