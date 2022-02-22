<script>
  let dialogue = [
    [`John`, `Hello. Can I help you?`],
    [`Ludwig`, `Are you Bertrand Russell, the greatest thinker of the age?`],
    [`John`, `No indeed! And what a preposterous proposition!`],
    [`Ludwig`, `Like you’re clever enough to be the judge of that.`],
    [
      `John`,
      `Another absurd suggestion! Make one more, young man, and I may have to have you arrested for spreading fake news.`,
    ],
    [`Ludwig`, `What’s fake news?`],
    [
      `John`,
      `I’m pleased you asked. Fake news is a term from the future. According to my rigorous calculations, the expression will enter the English language in 105 years – give or take a year or two.`,
    ],
    [`Ludwig`, `Surely it’s you that’s now being absurd.`],
    [
      `John`,
      `We’ll see. Anyway, I can’t quite place your accent. German, is it?`,
    ],
    [`Ludwig`, `Austrian, but I’ve been studying in Berlin.`],
    [`John`, `Studying what?`],
    [
      `Ludwig`,
      `Mechanical engineering mainly, but recently I’ve been getting heavily into mathematics.`,
    ],
    [`John`, `Which must be why you want to meet old Bertie.`],
    [
      `Ludwig`,
      `Exactly. Principia Mathematica is the greatest work of the age.`,
    ],
    [`John`, `You do like your superlatives, young man!`],
    [`Ludwig`, `Do you know where I can find him?`],
    [
      `John`,
      `You can usually find ‘the greatest thinker of the age’ in The Stumble Inn having tea and crumpets at this time of day.`,
    ],
    [
      `Ludwig`,
      `Thank you. Although it sounded like you put some of those words in quotation marks.`,
    ],
    [
      `John`,
      `Well spotted, young man. It seems you have a better ear for sarcasm than I would have expected, given your German background.`,
    ],
    [`Ludwig`, `Austrian, you mean.`],
    [`John`, `Whatever.`],
    [`Ludwig`, `So where can I find that place you mentioned?`],
    [
      `John`,
      `Go out of the front doors of the college over there and turn left. The Stumble Inn – you can’t miss it.`,
    ],
    [`Ludwig`, `Thank you. Should I tip you?`],
    [
      `John`,
      `Now you’re really starting to annoy me. Who did you think I was?`,
    ],
    [`Ludwig`, `I don’t know. The college porter?`],
    [
      `John`,
      `The porter? How dare you! I am John Maynard Keynes. John Maynard Keynes – the actual, real-life greatest thinker of the age! Without quotation marks! So why does everyone around here always think I’m the porter?`,
    ],
  ];

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
</script>

<div class="flex flex-col h-full">
  <div class="flex-grow overflow-auto">
    <div class="bg-blue-300 py-1">
      <h1 class="font-bold text-center">Flippin' English Club</h1>
    </div>
    <div class="font-mono leading-loose">
      {#each dialogue as line, i}
        <p
          class={i === lineI
            ? "p-2 bg-gray-200"
            : speechStatusStore[i] === "tolearn"
            ? "p-2 bg-red-100"
            : speechStatusStore[i] === "learning"
            ? "p-2 bg-yellow-100"
            : "p-2"}
        >
          <span on:click={() => selectLine(i)} class="font-bold cursor-pointer"
            >{line[speaker]}:
          </span>
          {#each line[speech].split(" ") as word, j}
            <span
              class={i === lineI && j === wordI
                ? "border-b-2 border-blue-300 rounded cursor-pointer pb-1"
                : "cursor-pointer pb-1"}
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

  <div class="px-3 py-2 bg-gray-700">
    <button
      class="mx-1 px-3 py-1 bg-green-300 rounded-md"
      on:click={showThreeWords}>+3</button
    >
    <button
      class="mx-1 px-3 py-1 bg-green-300 rounded-md"
      on:click={hideThreeWords}>-3</button
    >
    <button
      class="mx-1 px-3 py-1 bg-green-300 rounded-md"
      on:click={toggleSpeech}>All</button
    >
    <button
      class="mx-1 px-3 py-1 bg-green-300 rounded-md"
      on:click={toggleDialogue}>ALL!</button
    >
  </div>
</div>
