<script>
  import Header from "../components/Header.svelte";

  let pages = [
    {
      title: `#1 - Ludwig turns up at the wrong door`,
      slug: `1-ludwig-turns-up-at-the-wrong-door`,
    },
    {
      title: `#2 - Edward meets Aino and shares a secret`,
      slug: `2-edward-meets-aino-and-shares-a-secret`,
    },
    {
      title: `#3 - Five Finnish friends take a sauna`,
      slug: `3-five-finnish-friends-take-a-sauna`,
    },
  ];
</script>

<Header />

<div class="flex justify-center text-[1.1rem]">
  <div class="w-[800px]">
    <h1 class="mb-4 px-3 text-lg font-bold">Exercises</h1>
    <ul>
      {#each pages as { title, slug }}
        <li class="px-3">
          <a class="c-link" href={slug}>{title}</a>
        </li>
      {/each}
    </ul>
  </div>
</div>
