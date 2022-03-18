<script>
  import Header from "../components/Header.svelte";

  let toc = [
    {
      title: `#1 - Ch1 various`,
      slug: `s1`,
    },
    {
      title: `#2 - Ohjelmaa aamusta iltaan (p47)`,
      slug: `s2`,
    },
    {
      title: `#3 - Hei Hanna! Tänään alkaa Helsinki-viikko! (p48)`,
      slug: `s3`,
    },
    {
      title: `#4 - Taidenäyttelyssä (p50)`,
      slug: `s4`,
    },
  ];
</script>

<Header />

<div class="flex justify-center text-[1.1rem]">
  <div class="w-[800px]">
    <h1 class="mb-4 px-3 text-lg font-bold">Exercises</h1>
    {#each toc as { title, slug }}
      <a class="mb-1 block px-3 underline" href={slug}>{title}</a>
    {/each}
  </div>
</div>
