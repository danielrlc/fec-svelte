<script>
  import Flashcards from "../components/Flashcards.svelte";

  const content = {
    title: `#4 - Taidenäyttelyssä (p50)`,

    targetPhrases: [
      `Pedro ja Hanna ovat nykytaiteen museossa Kiasmassa.`,
      `Sinne on tänään vapaa pääsy, koska on Helsinki-päivä.`,
      `Näyttelyssä onkin paljon kävijöitä ja saleissa on ahdasta.`,
      `Puuh. Mua ärsyttää tää tungos.`,
      `Haluaks sä vielä katsoa jotain vai lähdetäänks jo?`,
      `No mua kyllä kiinnostaa vielä toi yläkerran näyttely.`,
      `Siellä on eteläamerikkalaisten taiteilijoiden videoteoksia.`,
      `No just. Et voi olla tosissas!`,
      `Mua väsyttää enkä mä jaksais enää kiertää täällä yhtään.`,
      `Mä en jotenki ymmärrä nykytaidetta ollenkaan.`,
      `Ai, miten niin?`,
      `No kato nyt tätäkin teosta: Kuka tahansa voi kaataa roskiksen sisällön lattialle ja sanoa, että se on taidetta!`,
      `Mua häiritsee, että nykytaide on niin harvoin kaunista.`,
      `Okei, no mä ymmärrän ton.`,
      `Eihän tää mikään kaunis teos ole.`,
      `Mut ehkä tää taiteilija onkin halunnut näyttää katsojalle maailman rumuutta ja likaa.`,
      `Tää teos panee meidät ajattelemaan.`,
      `Joo, no voi olla.`,
      `Mennäänks sit kuitenki yläkertaan?`,
      `No okei, mennään sit.`,
    ],

    sourcePhrases: [
      `Pedro and Hanna are at the Museum of Contemporary Art in Kiasma.`,
      `Admission is free today because it is Helsinki Day.`,
      `There are a lot of visitors to the exhibition and the halls are cramped.`,
      `Puuh. I'm annoyed by this crowd.`,
      `Would you like to see something again or leave already?`,
      `Well, I'm still interested in the upstairs exhibition.`,
      `There are video works by South American artists.`,
      `Honestly? You can't be serious!`,
      `I'm tired and I can't go around here anymore.`,
      `Somehow I don't understand contemporary art at all.`,
      `Oh, how so?`,
      `Well, look at this art work: Anyone can pour the contents of the trash on the floor and say it’s art!`,
      `It bothers me that contemporary art is so rarely beautiful.`,
      `Okay, well I understand that.`,
      `This is not a beautiful work.`,
      `But perhaps this artist has wanted to show the viewer the ugliness and dirt of the world.`,
      `This work makes us think.`,
      `Yeah, well it could be.`,
      `Shall we go upstairs anyway?`,
      `Well okay, let's go then.`,
    ],
  };
</script>

<Flashcards {...content} />
