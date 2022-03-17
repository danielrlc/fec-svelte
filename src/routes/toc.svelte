<script>
  import Header from "../components/Header.svelte";

  let toc = [
    {
      title: "#1 - Ch1 various",
      slug: "p1",
    },
    {
      title: "#2 - Ohjelmaa aamusta iltaan (p47)",
      slug: "p47",
    },
    {
      title: "#3 - Hei Hanna! Tänään alkaa Helsinki-viikko! (p48)",
      slug: "p48",
    },
  ];
</script>

<Header />

<div class="flex justify-center text-[1.1rem]">
  <div class="w-[800px]">
    <h1 class="text-lg font-bold px-3 mb-4">Exercises</h1>
    {#each toc as { title, slug }}
      <a class="block underline px-3 mb-1" href={slug}>{title}</a>
    {/each}
  </div>
</div>
