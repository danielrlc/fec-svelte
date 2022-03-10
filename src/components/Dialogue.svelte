<script>
  import Header from "./Header.svelte";
  import ControlPadButton from "./ControlPadButton.svelte";
  import Modal from "./Modal.svelte";

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
  let flipAllModalIsShown = false;

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
    flipAllModalIsShown = true;
    dialogueViewIsDim = true;
  }

  function hideFlipDialogueView() {
    flipAllModalIsShown = false;
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

    <div class="flex justify-center">
      <div class="max-w-2xl">
        <!-- Intro -->
        {#if introViewIsShown}
          <div class="px-3 u-text-ql">
            <h1 class="text-xl font-bold mb-2 py-5 lg:px-9 leading-6">
              {title}
            </h1>
            <h2 class="text-xl font-bold mb-3">Instructions</h2>
            <p class="mb-4">
              Learn the dialogue by guessing the hidden words, and then checking
              if you were correct. Leave hard-to-remember words or lines of dialogue hidden to come
              back to later.
            </p>
            <p class="mb-8">
              Or try reading a line of dialogue, and then hiding it to see how
              much you remember. Find out what combination works best for you.
            </p>
            <button
              on:click={endIntro}
              class="rounded-md bg-green-300 px-8 py-1">Start</button
            >
          </div>
        {/if}

        <!-- Dialogue -->
        {#if dialogueViewIsShown}
          <h1 class="text-xl font-bold mb-2 p-3 lg:px-9 leading-6">{title}</h1>
          <div class="leading-7 u-text-ql pb-8">
            {#each dialogue as line, i}
              <p
                class="pl-2 pr-3 lg:px-8 py-1 my-1 border-l-4 {speechStatusStore[
                  i
                ] === 'tolearn'
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
    </div>
  </div>

  <!-- Flip all modal -->
  {#if flipAllModalIsShown}
    <Modal
      on:showDialogue={showDialogue}
      on:hideDialogue={hideDialogue}
      on:cancel={hideFlipDialogueView}
    />
  {/if}

  <!-- Progress bar -->
  {#if dialogueViewIsShown}
    <div
      class="grid pt-1"
      style="grid-template-columns: repeat({speechCount}, 1fr);"
    >
      {#each speechStatusStore as phraseStatus, i}
        <span
          class="h-2 lg:h-3 {phraseStatus === 'tolearn'
            ? 'bg-red-300'
            : phraseStatus === 'learning'
            ? 'bg-yellow-300'
            : 'bg-green-300'} {i === lineI && 'border border-gray-700'}"
        />
      {/each}
    </div>

    <div class="text-center py-2">
      <div class="c-flex-center">
        <ControlPadButton
          label={hintsAreOn ? "No hints" : "Hints"}
          onClick={toggleHints}
          customClasses={"px-2-imp"}
        />

        <ControlPadButton label={"+3"} onClick={showThreeWords} />

        <ControlPadButton
          label={wholeLineIsHidden ? "Show" : "Hide"}
          onClick={toggleSpeech}
        />

        <ControlPadButton
          label={"=>"}
          onClick={goToNextLine}
          customClasses={"text-lg"}
        />

        <ControlPadButton
          label={"Flip all"}
          onClick={showFlipDialogueView}
          customClasses={"px-2-imp"}
        />

        <div class="flex flex-col content-center ml-3 leading-tight">
          <span>#{lineI + 1}</span>
          <span>{progress}%</span>
        </div>
      </div>
    </div>
  {/if}
</div>
