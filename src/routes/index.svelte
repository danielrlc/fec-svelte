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
  ];
</script>

<Header />

{#each pages as { title, slug }}
  <a class="block underline px-3 mb-4" href={slug}>{title}</a>
{/each}
