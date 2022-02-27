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
  let phraseCount = sourcePhrases.length

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

  function toggleWord(i) {
    wordI = i;
    wordStatusStore[phraseI][wordI] = !wordStatusStore[phraseI][wordI];
  }

  function showWord() {
    wordStatusStore[phraseI][wordI] = true;
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

  function showPhrase() {
    wordStatusStore[phraseI] = wordStatusStore[phraseI].map((_) => true);
  }

  function hidePhrase() {
    wordStatusStore[phraseI] = wordStatusStore[phraseI].map((_) => false);
  }

  $: wholePhraseIsHidden = wordStatusStore[phraseI].every(
    (status) => status === false
  );

  function togglePhrase() {
    wholePhraseIsHidden ? showPhrase() : hidePhrase();
    wordI = 0;
  }

  function toggleHints() {
    hintsAreOn = !hintsAreOn;
  }

  function goForward1() {
    phraseI = Math.min(phraseI + 1, phraseCount - 1);
  }

  $: progress = Math.round((phraseStatusStore
      .filter(phrase => phrase === 'learnt').length / phraseCount) * 100)
</script>

<div class="flex flex-col h-full">
  <div class="flex-grow overflow-auto">
    <Header />
    <div>
      <Title {title} />
      <p class="px-3 mb-4">{sourcePhrases[phraseI]}</p>
      <hr class="mb-4">
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
        {/each}
      </div>
    </div>
  </div>
  <div class="p-2 bg-gray-700 text-center">
    <div>
      <span class="text-white mr-2">{phraseI+1}/{phraseCount}</span>
      <ControlPadButton action={toggleHints} label="Hints" />
      <ControlPadButton action={showThreeWords} label="+3" />
      <ControlPadButton action={togglePhrase} label="All" />
      <ControlPadButton action={goForward1} label=">" />
      <span class="text-white ml-2">{progress}%</span>
    </div>
  </div>
</div>
