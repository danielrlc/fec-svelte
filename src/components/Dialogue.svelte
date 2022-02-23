<script>
  export let dialogue;

  let speaker = 0;
  let speech = 1;
  let lineI = 0;
  let wordI = 0;
  let hintsAreOn = true;

  let wordStatusStore = dialogue.map((line) =>
    line[speech].split(" ").map((_) => true)
  );

  $: speechStatusStore = wordStatusStore.map((statuses) =>
    statuses.every((status) => status === false)
      ? "tolearn"
      : statuses.every((status) => status === true)
      ? "learnt"
      : "learning"
  );

  function toggleWord(i, j) {
    lineI = i;
    wordI = j;
    wordStatusStore[lineI][wordI] = !wordStatusStore[lineI][wordI];
  }

  function showWord() {
    wordStatusStore[lineI][wordI] = true;
  }

  function hideWord() {
    wordStatusStore[lineI][wordI] = false;
  }

  function goToNextWord() {
    if (wordI < wordStatusStore[lineI].length - 1) {
      wordI++;
    }
  }

  function showThreeWords() {
    showWord();
    goToNextWord();
    showWord();
    goToNextWord();
    showWord();
    goToNextWord();
  }

  function hideThreeWords() {
    hideWord();
    goToNextWord();
    hideWord();
    goToNextWord();
    hideWord();
    goToNextWord();
  }

  function showSpeech() {
    wordStatusStore[lineI] = wordStatusStore[lineI].map((_) => true);
  }

  function hideSpeech() {
    wordStatusStore[lineI] = wordStatusStore[lineI].map((_) => false);
  }

  $: wholeSpeechIsHidden = wordStatusStore[lineI].every(
    (status) => status === false
  );

  $: wholeDialogueIsHidden = speechStatusStore.every(
    (status) => status === "tolearn"
  );

  function toggleSpeech() {
    wholeSpeechIsHidden ? showSpeech() : hideSpeech();
    wordI = 0;
  }

  function showDialogue() {
    wordStatusStore = dialogue.map((line) =>
      line[speech].split(" ").map((_) => true)
    );
  }

  function hideDialogue() {
    wordStatusStore = dialogue.map((line) =>
      line[speech].split(" ").map((_) => false)
    );
  }

  function toggleDialogue() {
    wholeDialogueIsHidden ? showDialogue() : hideDialogue();
  }

  function selectLine(i) {
    lineI = i;
    wordI = 0;
  }

  function toggleHints() {
    hintsAreOn = !hintsAreOn;
  }
</script>

<div class="flex flex-col h-full">
  <div class="flex-grow overflow-auto">
    <div class="bg-blue-300 py-1 mb-4">
      <p class="font-bold text-center">Flippin' English Club</p>
    </div>
    <div>
      <h1 class="text-xl font-bold mb-3 p-2">
        Ludwig turns up at the wrong door
      </h1>
      <div class="font-mono leading-7">
        {#each dialogue as line, i}
          <p
            class="p-2 {speechStatusStore[i] === 'tolearn' && i !== lineI
              ? 'bg-red-100'
              : speechStatusStore[i] === 'learning' &&
                i !== lineI &&
                'bg-yellow-100'}"
          >
            <span
              on:click={() => selectLine(i)}
              class="font-bold cursor-pointer"
              >{line[speaker]}:
            </span>
            {#each line[speech].split(" ") as word, j}
              <span
                class="cursor-pointer py-1 {i === lineI &&
                  j === wordI &&
                  'bg-green-200 rounded-md'}"
                on:click={() => toggleWord(i, j)}
                >{wordStatusStore[i][j]
                  ? word
                  : hintsAreOn
                  ? word
                      .split("")
                      .map((letter, k) => (k === 0 ? letter : "_"))
                      .join("")
                  : "____"}
              </span>
              <!-- Empty span needed to force space between words -->
              <span />
            {/each}
          </p>
        {/each}
      </div>
    </div>
  </div>
  <div class="p-2 bg-gray-700 text-center">
    <button
      class="w-12 mx-1 py-2 bg-green-300 rounded-md"
      on:click={showThreeWords}>+3</button
    >
    <button
      class="w-12 mx-1 py-2 bg-green-300 rounded-md"
      on:click={hideThreeWords}>-3</button
    >
    <button
      class="w-12 mx-1 py-2 bg-green-300 rounded-md"
      on:click={toggleSpeech}>All</button
    >
    <button
      class="w-12 mx-1 py-2 bg-green-300 rounded-md"
      on:click={toggleDialogue}>ALL!</button
    >
    <button
      class="w-12 mx-1 py-2 bg-green-300 rounded-md"
      on:click={toggleHints}>Hints</button
    >
  </div>
</div>
