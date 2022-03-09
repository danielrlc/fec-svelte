<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function showDialogue() {
    dispatch("showDialogue");
  }

  function hideDialogue() {
    dispatch("hideDialogue");
  }

  function cancel() {
    dispatch("cancel");
  }
</script>

<!-- Code taken from Tailwind UI modal example -->
<!-- https://tailwindui.com/components/application-ui/overlays/modals -->
<!-- This example requires Tailwind CSS v2.0+ -->
<div
  class="fixed z-10 inset-0 overflow-y-auto"
  aria-labelledby="modal-title"
  role="dialog"
  aria-modal="true"
>
  <div
    class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0"
  >
    <div
      class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
      aria-hidden="true"
    />
    <!-- This element is to trick the browser into centering the modal contents. -->
    <span
      class="hidden sm:inline-block sm:align-middle sm:h-screen"
      aria-hidden="true">&#8203;</span
    >
    <div
      class="relative inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full"
    >
      <div class="px-3 py-5 text-sm">
        <div class="mb-6">
          <h2 class="text-lg font-bold mb-1">Show dialogue</h2>
          <p class="mb-3">
            Show the whole dialogue if you just want to read it.
          </p>
          <button
            class="px-3 py-1 rounded-md bg-green-300"
            on:click={showDialogue}>Show dialogue</button
          >
        </div>

        <div class="mb-6">
          <h2 class="text-lg font-bold mb-1">Hide dialogue</h2>
          <p class="mb-3">
            Hide the whole dialogue if you want to start learning it from
            scratch again.
          </p>
          <button
            class="px-3 py-1 rounded-md bg-green-300"
            on:click={hideDialogue}>Hide dialogue</button
          >
        </div>

        <div class="mb-2">
          <h2 class="text-lg font-bold mb-1">Continue learning</h2>
          <p class="mb-3">Continue learning without changing anything.</p>
          <button class="px-3 py-1 rounded-md bg-red-300" on:click={cancel}
            >Continue learning</button
          >
        </div>
      </div>
    </div>
  </div>
</div>
