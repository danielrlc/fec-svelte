<script>
  export let onClick;
  export let label;
  export let customClasses = "";
  export let customIfClasses = "";

  const classes =
    "w-14 h-12 mx-1 px-1 rounded-md leading-none bg-gray-300 hover:bg-gray-200";
</script>

<button
  class="{classes} {customClasses} {customIfClasses}"
  on:click={onClick}
  >{label}
</button>
