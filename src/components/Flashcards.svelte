<script>
  import Header from "./Header.svelte";
  import Title from "./Title.svelte";
  import ControlPadButton from "./ControlPadButton.svelte";

  export let title;
  export let sourcePhrases;
  export let targetPhrases;

  let phraseI = 0;
  let wordI = 0;
  let hintsAreOn = false;
  let phraseCount = sourcePhrases.length;
  let introIsShown = true;
  let flashcardsAreShown = false;
  let progressMapIsShown = false;

  let wordStatusStore = targetPhrases.map((phrase) =>
    phrase.split(" ").map((_) => false)
  );

  $: phraseStatusStore = wordStatusStore.map((statuses) =>
    statuses.every((status) => status === false)
      ? "tolearn"
      : statuses.every((status) => status === true)
      ? "learnt"
      : "learning"
  );

  $: currentPhraseWordCount = wordStatusStore[phraseI].length;
  $: wholePhraseIsHidden = phraseStatusStore[phraseI] === "tolearn";
  $: wholePhraseIsShown = phraseStatusStore[phraseI] === "learnt";

  $: progress = Math.round(
    (phraseStatusStore.filter((phrase) => phrase === "learnt").length /
      phraseCount) *
      100
  );

  function toggleWord(i) {
    wordI = i;
    wordStatusStore[phraseI][wordI] = !wordStatusStore[phraseI][wordI];
  }

  function showWordAndGoToNext() {
    wordStatusStore[phraseI][wordI] = true;
    wordI < currentPhraseWordCount - 1 && wordI++;
  }

  function showThreeWords() {
    showWordAndGoToNext();
    showWordAndGoToNext();
    showWordAndGoToNext();
  }

  function showPhrase() {
    wordStatusStore[phraseI] = wordStatusStore[phraseI].map((_) => true);
  }

  function hidePhrase() {
    wordStatusStore[phraseI] = wordStatusStore[phraseI].map((_) => false);
  }

  function togglePhrase() {
    wholePhraseIsHidden ? showPhrase() : hidePhrase();
    wordI = 0;
  }

  function toggleHints() {
    hintsAreOn = !hintsAreOn;
  }

  function goForward1() {
    phraseI = Math.min(phraseI + 1, phraseCount - 1);
    wordI = 0;
  }

  function endIntro() {
    introIsShown = false;
    flashcardsAreShown = true;
  }

  function showFlashcards() {
    introIsShown = false;
    flashcardsAreShown = true;
    progressMapIsShown = false;
  }

  function showProgressMap() {
    introIsShown = false;
    flashcardsAreShown = false;
    progressMapIsShown = true;
  }

  function selectPhraseFromProgressMap(i) {
    phraseI = i;
    showFlashcards();
  }

  function toggleProgressMap() {
    progressMapIsShown ? showFlashcards() : showProgressMap();
  }
</script>

<div class="flex flex-col h-full">
  <div class="flex-grow overflow-auto">
    <!-- Intro -->
    {#if introIsShown}
      <Header />
      <Title {title} />
      <p class="px-3 mb-4">Instructions will be added here.</p>
      <button on:click={endIntro} class="mx-3 rounded-md bg-green-300 px-8 py-2"
        >Start</button
      >
    {/if}

    <!-- Progress map -->
    {#if progressMapIsShown}
      <Header />
      <div class="px-3 mb-2">
        <h2 class="text-xl font-bold mb-1">Progress map</h2>
        <p class="text-sm">Review your progress and pick your next phrase.</p>
      </div>

      <div class="grid grid-cols-10 gap-1 p-3">
        {#each phraseStatusStore as phraseStatus, i}
          <button
            class="c-flex-center h-8 rounded-md {phraseStatus === 'tolearn'
              ? 'bg-red-300'
              : phraseStatus === 'learning'
              ? 'bg-yellow-300'
              : 'bg-green-300'} {i === phraseI && 'border-4 border-gray-500'}"
            on:click={(_) => selectPhraseFromProgressMap(i)}
            >{phraseStatus === "tolearn"
              ? "–"
              : phraseStatus === "learning"
              ? "O"
              : "X"}</button
          >
        {/each}
      </div>
    {/if}

    <!-- Flashcard -->
    {#if flashcardsAreShown}
      <!-- Flashcard status bar -->
      <div
        class="h-1 {wholePhraseIsHidden
          ? 'bg-red-300'
          : wholePhraseIsShown
          ? 'bg-green-300'
          : 'bg-yellow-300'}"
      />

      <!-- Flashcard -->
      <div class="u-text-ql pb-8">
        <p class="px-3 my-5 leading-6">{sourcePhrases[phraseI]}</p>
        <hr class="mb-4" />
        <div class="px-3 leading-7">
          {#each targetPhrases[phraseI].split(" ") as word, i}
            <span
              class="cursor-pointer py-1 {i === wordI &&
                'bg-green-200 rounded-md'}"
              on:click={() => toggleWord(i)}
              >{wordStatusStore[phraseI][i]
                ? word
                : hintsAreOn
                ? word
                    .split("")
                    .map((letter, j) => (j === 0 ? letter : "_"))
                    .join("")
                : "_____"}
            </span>
            <span />
          {/each}
        </div>
      </div>
    {/if}
  </div>

  <!-- Progress bar -->
  {#if flashcardsAreShown || progressMapIsShown}
    <div
      class="grid border-y border-gray-500"
      style="grid-template-columns: repeat({phraseCount}, 1fr);"
    >
      {#each phraseStatusStore as phraseStatus, i}
        <span
          class="h-2 {phraseStatus === 'tolearn'
            ? 'bg-red-300'
            : phraseStatus === 'learning'
            ? 'bg-yellow-300'
            : 'bg-green-300'} {i === phraseI && 'border border-gray-500'}"
        />
      {/each}
    </div>
  {/if}

  <!-- Control pad -->
  {#if flashcardsAreShown || progressMapIsShown}
    <div class="text-center py-2">
      <div class="c-flex-center">
        <ControlPadButton
          label={hintsAreOn ? "No hints" : "Hints"}
          onClick={toggleHints}
          customIfClasses={progressMapIsShown && "c-disabled"}
        />

        <ControlPadButton
          label={"+3"}
          onClick={showThreeWords}
          customIfClasses={progressMapIsShown && "c-disabled"}
        />

        <ControlPadButton
          label={wholePhraseIsHidden ? "Words" : "No words"}
          onClick={togglePhrase}
          customIfClasses={progressMapIsShown && "c-disabled"}
        />

        <ControlPadButton
          label={"=>"}
          onClick={goForward1}
          customClasses={"text-lg"}
          customIfClasses={progressMapIsShown && "c-disabled"}
        />

        <ControlPadButton label={"Map/ Menu"} onClick={toggleProgressMap} />

        <div class="flex flex-col content-center ml-3 leading-tight">
          <span>#{phraseI + 1}</span>
          <span>{progress}%</span>
        </div>
      </div>
    </div>
  {/if}
</div>
