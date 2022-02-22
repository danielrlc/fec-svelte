<script>
  let dialogue = [
    [`John`, `Hello? Can I help you?`],
    [`Ludwig`, `Are you Bertrand Russell, the greatest thinker of the age?`],
  ];

  let speaker = 0;
  let speech = 1;
  let lineI = 0;
  let wordI = 0;
  let hintsAreOn = true;

  let wordStatusStore = dialogue.map((line) =>
    line[1].split(" ").map(_ => true)
  );

  function toggleWord(i, j) {
    lineI = i;
    wordI = j;
    wordStatusStore[lineI][wordI] = !wordStatusStore[lineI][wordI];
  }

  function toggleThreeWords() {
    wordStatusStore[lineI][wordI] = !wordStatusStore[lineI][wordI];
    if (wordI + 1 < wordStatusStore[lineI].length) {
      wordStatusStore[lineI][wordI + 1] = wordStatusStore[lineI][wordI];
    }
    if (wordI + 2 < wordStatusStore[lineI].length) {
      wordStatusStore[lineI][wordI + 2] = wordStatusStore[lineI][wordI];
    }
  }
</script>

<div class="p-3">
  <h1 class="font-bold mb-8">Flippin' English Club</h1>
  <div class="font-mono">
    {#each dialogue as line, i}
      <p class="mb-4">
        <span class="font-bold">{line[speaker]}: </span>
        {#each line[speech].split(" ") as word, j}
          <span class="cursor-pointer" on:click={(e) => toggleWord(i, j)}
            >{wordStatusStore[i][j]
              ? word
              : hintsAreOn
              ? word
                  .split("")
                  .map((letter, k) => (k === 0 ? letter : "_"))
                  .join("")
              : "____ "}
          </span>
          <!-- Empty span needed to force space between words -->
          <span />
        {/each}
      </p>
    {/each}
  </div>
</div>

<div class="p-3">
  <button class="px-3 py-1 bg-green-300" on:click={toggleThreeWords}
    >Toggle 3</button
  >
</div>
