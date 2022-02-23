<script>
  import Dialogue from "../components/Dialogue.svelte";

  let dialogue = [
    [`John`, `Hello. Can I help you?`],
    [`Ludwig`, `Are you Bertrand Russell, the greatest thinker of the age?`],
    [`John`, `No indeed! And what a preposterous proposition!`],
    [`Ludwig`, `Like you're clever enough to be the judge of that.`],
  ];
</script>

<Dialogue {dialogue} />
