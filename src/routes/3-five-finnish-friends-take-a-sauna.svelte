<script>
  import Header from "../components/Header.svelte";
  import Title from "../components/Title.svelte";

  let dialogueIsShown = false;

  function showDialogue() {
    dialogueIsShown = true;
  }
</script>

<Header />

<div class="flex justify-center">
  <div class="w-[800px] px-3 text-[1.1rem] mb-16">
    <Title title="#3 - Five Finnish friends take a sauna" />
    <p class="mb-3">
      <a
        class="text-blue-700 underline"
        href="https://en.wikipedia.org/wiki/Arthur_Dent">Arthur Dent</a
      > could never get the hang of Thursdays. But that's not true of the five Finnish
      friends featured in this dialogue, who took a sauna together on a Thursday
      evening after work. The conversation flowed as they discussed the pressing
      issues of the day.
    </p>
    <p class="mb-8">Let's pick up the conversation halfway through...</p>

    {#if !dialogueIsShown}
      <button
        class="rounded-md bg-green-300 px-6 py-2 hover:bg-green-400"
        on:click={showDialogue}>Read the dialogue</button
      >
    {/if}

    {#if dialogueIsShown}
      <p class="mb-3">
        <span class="font-bold">Sauna stove:</span>
        <span>(hissing sound)</span>
      </p>
      <p class="mb-3">...</p>
      <p class="mb-3">
        <span class="font-bold">Crickets outside:</span>
        <span>(chirping)</span>
      </p>
      <p class="mb-3">...</p>
      <p class="mb-3">
        <span class="font-bold">Sauna stove:</span>
        <span>(more hissing)</span>
      </p>
      <p class="mb-3">...</p>
      <p class="mb-3">
        <span class="font-bold">Crickets outside:</span>
        <span>(more chirping)</span>
      </p>
    {/if}
  </div>
</div>
