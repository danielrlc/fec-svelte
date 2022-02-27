<script>
  import Header from "../components/Header.svelte";

  let pages = [
    {
      title: "#1 - Ludwig turns up at the wrong door",
      slug: "1-ludwig-turns-up-at-the-wrong-door",
    },
    {
      title: "#2 - Spoken phrases (placeholder content)",
      slug: "2-spoken-phrases",
    },
  ];
</script>

<Header />

{#each pages as { title, slug }}
  <a class="block underline px-3 mb-4" href={slug}>{title}</a>
{/each}
