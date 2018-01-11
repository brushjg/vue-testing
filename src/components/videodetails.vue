<template>
  <div class="videoarea">
    <iframe class="embed-responsive-item" :src="activeVideoIDC" ></iframe>
  </div>
</template>
<script>
  export default {
    props: {
      activeVideoIDC: {
        type: String,
        required: true
      }
    }
  }
</script>
