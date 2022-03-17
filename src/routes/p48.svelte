<script>
  import Flashcards from "../components/Flashcards.svelte";

  const content = {
    title: `#3 - Hei Hanna! Tänään alkaa Helsinki-viikko! (p48)`,

    targetPhrases: [
      `Hei Hanna!`,
      `Tänään alkaa Helsinki-viikko!`,
      `Mennään katsomaan jotain esitystä!`,
      `Joo, mennään vaan.`,
      `Mitä ohjelmaa siel on?`,
      `Vaikka mitä?`,
      `Keskustassa on ainakin teatteria ja konsertti.`,
      `Vai lähdetäänks pelaamaan rantalentistä?`,
      `Mennään vaan!`,
      `Olis kiva pelata, kun on näin hyvä ilmakin.`,
      `Joo, tehdään niin.`,
      `Ja illalla katsotaan sit leffa Senaatintorilla!`,
      `Ai ulkona, vau!`,
      `Mikä leffa siel näytetään?`,
      `Joku Kaurismäen filmi.`,
      `Mä en ole vielä nähnyt yhtään Kaurismäen leffaa.`,
      `Siksi mä haluaisin nähdä tän.`,
      `Okei, sopii mulle.`,
      `Täytyy varmaan mennä ajoissa, et saadaan hyvät paikat.`,
      `Hey Hanna!`,
    ],

    sourcePhrases: [
      `Helsinki Week starts today!`,
      `Let's go see a show!`,
      `Yeah, let's just go.`,
      `What's on the program?`,
      `All kinds?`,
      `There is at least some theatre and a concert in the centre.`,
      `Or let's start playing on the beach?`,
      `Let's go!`,
      `It would be nice to play when the weather is so good.`,
      `Yeah, let's do that.`,
      `And in the evening, watch a movie at Senate Square!`,
      `Oh outside, Wow!`,
      `Which movie will be shown?`,
      `Some Kaurismäki film.`,
      `I haven't seen any Kaurismäki movies yet.`,
      `That's why I'd like to see this.`,
      `Okay, that sounds good to me.`,
      `Let's go in good time, or we won't get good places.`,
    ],
  };
</script>

<Flashcards {...content} />
