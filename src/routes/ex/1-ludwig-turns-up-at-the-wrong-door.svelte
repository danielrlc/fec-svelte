<script>
  import Dialogue from "../../components/Dialogue.svelte";

  const content = {
    title: "#1 - Ludwig turns up at the wrong door",

    dialogue: [
      [`John`, `Hello. Can I help you?`],
      [`Ludwig`, `Are you Bertrand Russell, the greatest thinker of the age?`],
      [`John`, `No indeed! And what a preposterous proposition!`],
      [`Ludwig`, `Like you're clever enough to be the judge of that.`],
      [
        `John`,
        `Another absurd suggestion! Make one more, young man, and I may have to have you arrested for spreading fake news.`,
      ],
      [`Ludwig`, `What's fake news?`],
      [
        `John`,
        `I'm pleased you asked. Fake news is a term from the future. According to my rigorous calculations, the expression will enter the English language in 105 years – give or take a year or two.`,
      ],
      [`Ludwig`, `Surely it's you that's now being absurd.`],
      [
        `John`,
        `We'll see. Anyway, I can't quite place your accent. German, is it?`,
      ],
      [`Ludwig`, `Austrian, but I've been studying in Berlin.`],
      [`John`, `Studying what?`],
      [
        `Ludwig`,
        `Mechanical engineering mainly, but recently I've been getting heavily into mathematics.`,
      ],
      [`John`, `Which must be why you want to meet old Bertie.`],
      [
        `Ludwig`,
        `Exactly. Principia Mathematica is the greatest work of the age.`,
      ],
      [`John`, `You do like your superlatives, young man!`],
      [`Ludwig`, `Do you know where I can find him?`],
      [
        `John`,
        `You can usually find ‘the greatest thinker of the age' in The Stumble Inn having tea and crumpets at this time of day.`,
      ],
      [
        `Ludwig`,
        `Thank you. Although it sounded like you put some of those words in quotation marks.`,
      ],
      [
        `John`,
        `Well spotted, young man. It seems you have a better ear for sarcasm than I would have expected, given your German background.`,
      ],
      [`Ludwig`, `Austrian, you mean.`],
      [`John`, `Whatever.`],
      [`Ludwig`, `So where can I find that place you mentioned?`],
      [
        `John`,
        `Go out of the front doors of the college over there and turn left. The Stumble Inn – you can't miss it.`,
      ],
      [`Ludwig`, `Thank you. Should I tip you?`],
      [
        `John`,
        `Now you're really starting to annoy me. Who did you think I was?`,
      ],
      [`Ludwig`, `I don't know. The college porter?`],
      [
        `John`,
        `The porter? How dare you! I am John Maynard Keynes. John Maynard Keynes – the actual, real-life greatest thinker of the age! Without quotation marks! So why does everyone around here always think I'm the porter?`,
      ],
    ],
  };
</script>

<Dialogue {...content} />
