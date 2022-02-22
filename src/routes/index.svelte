<script>
  let dialogue = [
    [`John`, `Hello? Can I help you?`],
    [`Ludwig`, `Are you Bertrand Russell, the greatest thinker of the age?`],
  ];

  let speaker = 0;
  let speech = 1;
  let lineI = 0;
  let wordI = 0;
  let hintsAreOn = false;

  let wordStatusStore = dialogue.map((line) =>
    line[1].split(" ").map((_) => true)
  );

  function toggleWord(i, j) {
    lineI = i;
    wordI = j;
    wordStatusStore[lineI][wordI] = !wordStatusStore[lineI][wordI];
  }

  function showWord() {
    wordStatusStore[lineI][wordI] = true
  }

  function hideWord() {
    wordStatusStore[lineI][wordI] = false
  }

  function goToNextWord() {
    if (wordI < wordStatusStore[lineI].length - 1) {
      wordI++
    }
  }

  function showThreeWords() {
    showWord()
    goToNextWord()
    showWord()
    goToNextWord()
    showWord()
    goToNextWord()
  }

  function hideThreeWords() {
    hideWord()
    goToNextWord()
    hideWord()
    goToNextWord()
    hideWord()
    goToNextWord()
  }

</script>

<div class="p-3">
  <h1 class="font-bold mb-8">Flippin' English Club</h1>
  <div class="font-mono">
    {#each dialogue as line, i}
      <p class="mb-4">
        <span class="font-bold">{line[speaker]}: </span>
        {#each line[speech].split(" ") as word, j}
          <span
            class={i === lineI && j === wordI
              ? "border-b-2 border-blue-300 rounded cursor-pointer pb-1"
              : "cursor-pointer pb-1"}
            on:click={(e) => toggleWord(i, j)}
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
  <button class="px-3 py-1 bg-green-300" on:click={showThreeWords}
    >+3</button
  >
  <button class="px-3 py-1 bg-green-300" on:click={hideThreeWords}
    >-3</button
  >
</div>
