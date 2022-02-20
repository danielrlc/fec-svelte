<script>
  let dialogue = [
    [`John`, `Hello? Can I help you?`],
    [`Ludwig`, `Are you Bertrand Russell, the greatest thinker of the age?`],
  ];
  let speaker = 0
  let speech = 1
  let wordStatusRegister = dialogue.map((speech) =>
    speech[1].split(" ").map((word) => true)
  );
  let hintsAreOn = false;
  function toggleWord(i, j) {
    wordStatusRegister[i][j] = !wordStatusRegister[i][j];
  }
</script>

<div class="text-center text-2xl py-4">
  <h1 class="font-bold mb-8">Flippin' English Club</h1>
  <p class="font-mono">
    {#each dialogue as line, i}
      <span class="font-bold">{line[speaker]}: </span>
      {#each line[speech].split(" ") as word, j}
        <span on:click={(e) => toggleWord(i, j)}
          >{wordStatusRegister[i][j]
            ? word
            : hintsAreOn
            ? word
                .split("")
                .map((letter, k) => (k === 0 ? letter : "_"))
                .join("")
            : "____ "}
        </span>
      {/each}
    {/each}
  </p>
</div>
