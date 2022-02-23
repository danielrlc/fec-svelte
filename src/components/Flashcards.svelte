<script>
  import Header from "./Header.svelte";
  import Title from "./Title.svelte";
  import ControlPadButton from "./ControlPadButton.svelte";

  export let title;
  export let sourcePhrases;
  export let targetPhrases;

  let phraseI = 0;
  let wordI = 0;
  let hintsAreOn = true;
  let phraseCount = sourcePhrases.length

  let wordStatusStore = targetPhrases.map((phrase) =>
    phrase.split(" ").map((_) => true)
  );

  $: phraseStatusStore = wordStatusStore.map((statuses) =>
    statuses.every((status) => status === false)
      ? "tolearn"
      : statuses.every((status) => status === true)
      ? "learnt"
      : "learning"
  );

  function toggleWord(i) {
    wordI = i;
    wordStatusStore[phraseI][wordI] = !wordStatusStore[phraseI][wordI];
  }

  function showWord() {
    wordStatusStore[phraseI][wordI] = true;
  }

  function hideWord() {
    wordStatusStore[phraseI][wordI] = false;
  }

  function goToNextWord() {
    if (wordI < wordStatusStore[phraseI].length - 1) {
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

  function showPhrase() {
    wordStatusStore[phraseI] = wordStatusStore[phraseI].map((_) => true);
  }

  function hidePhrase() {
    wordStatusStore[phraseI] = wordStatusStore[phraseI].map((_) => false);
  }

  $: wholePhraseIsHidden = wordStatusStore[phraseI].every(
    (status) => status === false
  );

  $: allPhrasesAreHidden = phraseStatusStore.every(
    (status) => status === "tolearn"
  );

  function togglePhrase() {
    wholePhraseIsHidden ? showPhrase() : hidePhrase();
    wordI = 0;
  }

  function showAllPhrases() {
    wordStatusStore = targetPhrases.map((phrase) =>
      phrase.split(" ").map((_) => true)
    );
  }

  function hideAllPhrases() {
    wordStatusStore = targetPhrases.map((phrase) =>
      phrase.split(" ").map((_) => false)
    );
  }

  function toggleAllPhrases() {
    allPhrasesAreHidden ? showAllPhrases() : hideAllPhrases();
  }

  function toggleHints() {
    hintsAreOn = !hintsAreOn;
  }

  function goBack10() {
    phraseI = Math.max(phraseI - 10, 0);
  }

  function goBack1() {
    phraseI = Math.max(phraseI - 1, 0);
  }

  function goForward1() {
    phraseI = Math.min(phraseI + 1, phraseCount - 1);
  }

  function goForward10() {
    phraseI = Math.min(phraseI + 10, phraseCount - 1);
  }
</script>

<div class="flex flex-col h-full">
  <div class="flex-grow overflow-auto">
    <Header />
    <div>
      <Title {title} />
      <p>{sourcePhrases[phraseI]}</p>
      <div class="font-mono leading-7">
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
              : "____"}
          </span>
          <!-- Empty span needed to force space between words -->
          <span />
        {/each}
      </div>
    </div>
  </div>
  <div class="p-2 bg-gray-700 text-center">
    <div class="mb-2">
      <ControlPadButton action={goBack10} label="<<" />
      <ControlPadButton action={goBack1} label="<" />
      <span class="text-white">{phraseI+1}/{phraseCount}</span>
      <ControlPadButton action={goForward1} label=">" />
      <ControlPadButton action={goForward10} label=">>" />
    </div>
    <div>
      <ControlPadButton action={showThreeWords} label="+3" />
      <ControlPadButton action={hideThreeWords} label="-3" />
      <ControlPadButton action={togglePhrase} label="All" />
      <ControlPadButton action={toggleAllPhrases} label="ALL!" />
      <ControlPadButton action={toggleHints} label="Hints" />
    </div>
  </div>
</div>
