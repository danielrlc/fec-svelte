<script>
  import Header from "./Header.svelte";
  import Title from "./Title.svelte";
  import ControlPadButton from "./ControlPadButton.svelte";
  import Modal from "./Modal.svelte";

  export let title;
  export let preamble;
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

<div class="flex h-full flex-col">
  <div class="flex-grow overflow-auto">
    <Header />

    <div class="flex justify-center">
      <div class="w-[800px]">
        <!-- Intro -->
        {#if introViewIsShown}
          <div class="px-3 text-[1.1rem]">
            <Title {title} />

            <h2 class="mb-3 text-xl font-bold">Quick start</h2>
            <p class="c-p mb-5">
              Learn the dialogue by guessing the hidden words, and then
              revealing them to check if you were correct.
            </p>
            <button
              on:click={endIntro}
              class="mb-10 rounded-md bg-green-300 px-8 py-1">Start</button
            >

            <h2 class="mb-3 text-xl font-bold">Learning tips</h2>
            <p class="c-p">
              Turn on the hints to help you learn a new sentence.
            </p>
            <p class="c-p">
              Reveal the sentence a word at a time, three words at a time, or
              all at once.
            </p>
            <p class="c-p">
              Leave hard-to-remember words hidden to come back to later.
            </p>
            <p class="c-p">
              Read a line of dialogue, then hide it and see how much you
              remember.
            </p>
          </div>
        {/if}

        <!-- Dialogue -->
        {#if dialogueViewIsShown}
          <Title {title} customClasses="px-3" />

          {#if preamble}
            <p class="mb-4 px-3 italic">{preamble}</p>
          {/if}

          <div class="pb-8 text-[1.1rem] leading-7">
            {#each dialogue as line, i}
              <p
                class="my-1 border-l-4 py-1 pl-2 pr-3 lg:px-8 {speechStatusStore[
                  i
                ] === 'tolearn'
                  ? 'border-red-300'
                  : speechStatusStore[i] === 'learning'
                  ? 'border-yellow-300'
                  : 'border-green-300'}"
              >
                <span
                  on:click={() => selectLine(i)}
                  class="cursor-pointer font-bold"
                  >{line[speaker]}:
                </span>
                {#each line[speech].split(" ") as word, j}
                  <span
                    class="cursor-pointer py-1 {i === lineI &&
                      j === wordI &&
                      'rounded-md bg-green-200'}"
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

    <div class="py-2 text-center">
      <div class="c-flex-center">
        <ControlPadButton
          label={hintsAreOn ? "No hints" : "Hints"}
          onClick={toggleHints}
          customClasses="!px-2"
        />

        <ControlPadButton label="+3" onClick={showThreeWords} />

        <ControlPadButton
          label={wholeLineIsHidden ? "Show" : "Hide"}
          onClick={toggleSpeech}
        />

        <ControlPadButton
          label="=>"
          onClick={goToNextLine}
          customClasses="text-lg"
        />

        <ControlPadButton
          label="Flip all"
          onClick={showFlipDialogueView}
          customClasses="!px-2"
        />

        <div class="ml-3 flex flex-col content-center leading-tight">
          <span>#{lineI + 1}</span>
          <span>{progress}%</span>
        </div>
      </div>
    </div>
  {/if}
</div>
