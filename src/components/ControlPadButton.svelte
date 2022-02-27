<script>
  export let action
  export let label
</script>

<button class="w-11 mx-1 py-2 bg-green-300 rounded-md" on:click={action}
  >{label}</button
>
