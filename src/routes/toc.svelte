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
    {
      title: `#5 - Kauas pilvet karkaavat (p59)`,
      slug: `s5`,
    },
  ];
</script>

<Header />

<div class="flex justify-center text-[1.1rem]">
  <div class="w-[800px]">
    <h1 class="mb-4 px-3 text-lg font-bold">Exercises</h1>
    <ul>
      {#each toc as { title, slug }}
        <li class="px-3">
          <a class="c-link" href={slug}>{title}</a>
        </li>
      {/each}
    </ul>
  </div>
</div>
