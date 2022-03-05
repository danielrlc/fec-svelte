<script>
  import Header from "./Header.svelte";
  import Title from "./Title.svelte";

  export let title;
  export let dialogue;

  let speaker = 0;
  let speech = 1;
  let lineI = 0;
  let wordI = 0;
  let speechCount = dialogue.length;
  let hintsAreOn = true;
  let introViewIsShown = true;
  let dialogueViewIsShown = false;
  let flipDialogueViewIsShown = false;

  let wordStatusStore = dialogue.map((line) =>
    line[speech].split(" ").map((_) => false)
  );

  $: currentPhraseWordCount = wordStatusStore[lineI].length;

  $: speechStatusStore = wordStatusStore.map((statuses) =>
    statuses.every((status) => status === false)
      ? "tolearn"
      : statuses.every((status) => status === true)
      ? "learnt"
      : "learning"
  );

  $: wholeLineIsHidden = speechStatusStore[lineI] === "tolearn";

  $: progress = Math.round(
    (speechStatusStore.filter((speech) => speech === "learnt").length /
      speechCount) *
      100
  );

  function toggleWord(i, j) {
    lineI = i;
    wordI = j;
    wordStatusStore[lineI][wordI] = !wordStatusStore[lineI][wordI];
  }

  function showWordAndGoToNext() {
    wordStatusStore[lineI][wordI] = true;
    wordI < currentPhraseWordCount - 1 && wordI++;
  }

  function showThreeWords() {
    showWordAndGoToNext();
    showWordAndGoToNext();
    showWordAndGoToNext();
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

  function toggleSpeech() {
    wholeSpeechIsHidden ? showSpeech() : hideSpeech();
    wordI = 0;
  }

  function showDialogue() {
    wordStatusStore = dialogue.map((line) =>
      line[speech].split(" ").map((_) => true)
    );
    lineI = 0;
    wordI = 0;
    hideFlipDialogueView();
  }

  function hideDialogue() {
    wordStatusStore = dialogue.map((line) =>
      line[speech].split(" ").map((_) => false)
    );
    lineI = 0;
    wordI = 0;
    hideFlipDialogueView();
  }

  function showFlipDialogueView() {
    flipDialogueViewIsShown = true;
    dialogueViewIsDim = true;
  }

  function hideFlipDialogueView() {
    flipDialogueViewIsShown = false;
    dialogueViewIsDim = false;
  }

  function selectLine(i) {
    lineI = i;
    wordI = 0;
  }

  function toggleHints() {
    hintsAreOn = !hintsAreOn;
  }

  function endIntro() {
    introViewIsShown = false;
    dialogueViewIsShown = true;
  }

  function goToNextLine() {
    lineI = Math.min(lineI + 1, speechCount - 1);
    wordI = 0;
  }
</script>

<div class="flex flex-col h-full">
  <div class="flex-grow overflow-auto">
    <Header />

    <!-- Intro -->
    {#if introViewIsShown}
      <div class="px-3 u-text-ql">
        <h2 class="text-xl font-bold mb-3">Instructions</h2>
        <p class="mb-4">
          In this exercise, you can hide and show words and whole lines of
          dialogue. Try to work out the next word or line, then show it and see
          if you were correct. If you get it wrong, hide the word or line again
          and come back to it a bit later.
        </p>
        <p class="mb-8">Repeat this process through the whole dialogue.</p>
        <button on:click={endIntro} class="rounded-md bg-green-300 px-8 py-1"
          >Start</button
        >
      </div>
    {/if}

    <!-- Dialogue -->
    {#if dialogueViewIsShown}
      <Title {title} />
      <div class="leading-7 u-text-ql">
        {#each dialogue as line, i}
          <p
            class="px-2 py-1 my-1 border-l-4 {speechStatusStore[i] === 'tolearn'
              ? 'border-red-300'
              : speechStatusStore[i] === 'learning'
              ? 'border-yellow-300'
              : 'border-green-300'}"
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
    {/if}
  </div>

  <!-- Toggle dialogue confirm popup -->
  {#if flipDialogueViewIsShown}
    <div class="h-full bg-gray-100 text-sm absolute z-10 px-3 py-6">
      <div class="mb-6">
        <h2 class="text-lg font-bold mb-1">Show dialogue</h2>
        <p class="mb-3">Show the whole dialogue if you just want to read it.</p>
        <button
          class="px-3 py-1 rounded-md bg-green-300"
          on:click={showDialogue}>Show dialogue</button
        >
      </div>

      <div class="mb-6">
        <h2 class="text-lg font-bold mb-1">Hide dialogue</h2>
        <p class="mb-3">
          Hide the whole dialogue if you want to start learning it from scratch
          again.
        </p>
        <button
          class="px-3 py-1 rounded-md bg-green-300"
          on:click={hideDialogue}>Hide dialogue</button
        >
      </div>

      <div class="mb-2">
        <h2 class="text-lg font-bold mb-1">Continue learning</h2>
        <p class="mb-3">Continue learning without changing anything.</p>
        <button
          class="px-3 py-1 rounded-md bg-red-300"
          on:click={hideFlipDialogueView}>Continue learning</button
        >
      </div>
    </div>
  {/if}

  <!-- Progress bar -->
  {#if dialogueViewIsShown}
    <div
      class="grid grid-cols-10"
      style="grid-template-columns: repeat({speechCount}, 1fr);"
    >
      {#each speechStatusStore as phraseStatus, i}
        <span
          class="h-2 {phraseStatus === 'tolearn'
            ? 'bg-red-300'
            : phraseStatus === 'learning'
            ? 'bg-yellow-300'
            : 'bg-green-300'} {i === lineI && 'border border-gray-700'}"
        />
      {/each}
    </div>

    <div class="p-1 text-center text-sm">
      <div class="c-flex-center">
        <button class="c-flashcards-btn bg-gray-200" on:click={toggleHints}
          >{hintsAreOn ? "No hints" : "Hints"}</button
        >

        <button class="c-flashcards-btn bg-gray-200" on:click={showThreeWords}
          >+3</button
        >

        <button class="c-flashcards-btn bg-gray-200" on:click={toggleSpeech}
          >{wholeLineIsHidden ? "Show" : "Hide"}</button
        >

        <button class="c-flashcards-btn bg-gray-200" on:click={goToNextLine}
          >=></button
        >

        <button
          class="c-flashcards-btn bg-gray-200"
          on:click={showFlipDialogueView}>ALL</button
        >

        <div class="flex flex-col content-center ml-3 leading-snug">
          <span>#{lineI + 1}</span>
          <span>{progress}%</span>
        </div>
      </div>
    </div>
  {/if}
</div>
