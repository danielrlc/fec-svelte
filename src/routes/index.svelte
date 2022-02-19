<script>
  let sentence = "Mikä sinun nimesi on?";
  let wordStatusRegister = sentence.split(" ").map((word) => true);
  function toggleWord(i) {
    wordStatusRegister[i] = !wordStatusRegister[i];
  }
</script>

<h1>Welcome to SvelteKit</h1>
<p>
  {#each sentence.split(" ") as word, i}
    <span on:click={e => toggleWord(i)}
      >{wordStatusRegister[i] ? word : "____ "}
    </span>
  {/each}
</p>

<style>
  p {
    font-size: 1.5rem;
    font-family: monospace;
  }
</style>
