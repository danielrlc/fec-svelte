<script>
  import Header from "../components/Header.svelte";

  let pages = [
    {
      title: "#1 - Ludwig turns up at the wrong door",
      slug: "1-ludwig-turns-up-at-the-wrong-door",
    },
    {
      title: "#2 - Edward meets Aino and shares a secret",
      slug: "2-edward-meets-aino-and-shares-a-secret",
    },
    {
      title: "#3 - Five Finnish friends take a sauna",
      slug: "3-five-finnish-friends-take-a-sauna",
    },
  ];
</script>

<Header />

<div class="flex justify-center text-[1.1rem]">
  <div class="w-[800px]">
    <h1 class="text-lg font-bold px-3 mb-4">Exercises</h1>
    {#each pages as { title, slug }}
      <a class="block underline px-3 mb-1" href={slug}>{title}</a>
    {/each}
  </div>
</div>
