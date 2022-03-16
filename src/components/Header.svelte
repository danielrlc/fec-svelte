<script>
  function goFullScreen() {
    document.body.requestFullscreen();
  }
</script>

<div class="mb-6 bg-blue-300 py-1 px-3 lg:mb-10 lg:px-8">
  <a href="/" class="text-center font-bold hover:underline"
    >Flippin' English Club</a
  >
  <button on:click={goFullScreen}>Go fullscreen</button>
</div>
