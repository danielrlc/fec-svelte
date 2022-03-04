<script>
  import Dialogue from "../components/Dialogue.svelte";

  const content = {
    title: "#2 - Edward meets Aino and shares a secret",

    dialogue: [
      [`Aino`, `Hello? Can I help you?`],
      [`Edward`, `Hello. Is this where Jean Sibelius lives? Are you his wife?`],
      [`Aino`, `Yes, I'm Aino. Jean is out in the garden chopping firewood.`],
      [`Edward`, `Ah, so this house must be named after you.`],
      [`Aino`, `That's right. Ainola means “Aino's place”.`],
      [
        `Edward`,
        `I am Edward, Edward Elgar, and I'm very pleased to meet you.`,
      ],
      [`Aino`, `Pleased to meet you. May I call you Edward?`],
      [`Edward`, `I would like that very much. And may I call you Aino?`],
      [
        `Aino`,
        `I would like that, too. So you are the great English composer that Jean can't stop talking about!`,
      ],
      [`Edward`, `You're very kind.`],
      [
        `Aino`,
        `Not at all! We're both huge fans of your Enigma Variations. But tell me, what exactly is the big “Enigma”? That means mystery, doesn't it?`,
      ],
      [
        `Edward`,
        `That's right, and I would love to tell you the answer, but then I would have to kill you.`,
      ],
      [
        `Aino`,
        `Well, how about you just whisper it to me so my daughters don't hear? I promise I won't tell Jean if you don't want me to.`,
      ],
      [
        `Edward`,
        `Why not? I rather like the idea of your knowing the riddle, and your husband not.`,
      ],
      [`Aino`, `So do I!`],
      [`Edward`, `(Whispers in Aino's ear.)`],
      [
        `Aino`,
        `Wow! I was not expecting that! I didn't know Oscar Wilde was a composer as well as a writer.`,
      ],
      [
        `Edward`,
        `Shhhh! Nor did I. He prefered to keep that private for some reason. Anyway, please keep schtum. I don't want the whole world to know.`,
      ],
      [`Aino`, `Don't worry, your secret is safe with me.`],
      [
        `Edward`,
        `You have a very beautiful home here, Aino. What a lovely view you have of the lake there!`,
      ],
      [
        `Aino`,
        `Yes, that was something we asked the architect to include in the design. We also had a special fireplace put into the dining room, but I'll let Jean show you that. It's his pride and joy, and he loves showing it off to his friends, especially if they're musicians themselves.`,
      ],
      [
        `Edward`,
        `I look forward to that. If you'll excuse me, I think I'll go out and find him in the garden. I can hear the sound of an axe over there.`,
      ],
      [
        `Aino`,
        `I should warn you, whenever he goes to chop firewood, it's because he's got into one of his moods.`,
      ],
      [`Edward`, `Oh dear! Well, maybe I can go and pull him out of it.`],
      [`Aino`, `I wish you good luck with that!`],
      [
        `Edward`,
        `It sounds like I'm going to need it! I'll go and find him now then.`,
      ],
      [`Aino`, `Good idea, and you must stay for dinner this evening, Edward.`],
      [`Edward`, `Thank you, Aino. I would like that very much.`],
    ],
  };
</script>

<Dialogue {...content} />
