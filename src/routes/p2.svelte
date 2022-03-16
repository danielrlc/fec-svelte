<script>
  import Flashcards from "../components/Flashcards.svelte";

  const content = {
    title: `#P2: Ohjelmaa aamusta iltaan`,

    targetPhrases: [
      `Ohjelmaa aamusta iltaan`,
      `Helsinki-viikko starttaa tänään`,
      `Perinteistä Helsinki-päivää vietetään tänä vuonna kokonainen viikko.`,
      `Tapahtuman järjestäjät ovat halunneet, että ihmiset voisivat liittyä mukaan helposti, vaikkapa kesken ostosreissun tai työmatkan.`,
      `Siksi ohjelmassa on paljon ulkoilmatapahtumia keskellä kaupunkia.`,
      `Tänään lauantaina, festivaalin aloituspäivänä, ohjelmaa on eniten.`,
      `Juhlallisuudet alkavat Senaatintorilla kello 12, jolloin kaupunginjohtaja pitää puheen ja Helsingin kaupunginorkesteri soittaa juhlakonsertin.`,
      `Tuomiokirkon portaat on varattu yleisölle, sillä tapahtumaan odotetaan valtavasti katsojia.`,
      `Senaatintorilla tarjoillaan myös 1800-luvun kahvilaherkkuja viihtyisässä vanhanaikaisessa torikahvilassa.`,
      `Päivän aikana keskustassa tapahtuu paljon: Rautatientorilla voi opetella paritansseja ja Hietaniemen rannalla pelataan rantalentopallon kaupunki-cup, johon kuka tahansa voi osallistua.`,
      `Esplanadin puistossa keskitytään kulttuuriin: Runebergin patsaalla lausutaan runoja, Espan lavalla esitetään improvisaatioteatteria ja lisäksi ohikulkijat voivat kirjoittaa Helsinki-aiheiset muistonsa jättikokoiseen kirjaan.`,
      `Kirja julkaistaan syksyllä nimellä Minun Helsinkini.`,
      `Kello 22 Senaatintorin lava muuttuu elokuvanäyttämöksi.`,
      `Siellä näytetään joka ilta yksi Helsinki-aiheinen elokuva.`,
      `Tänään on vuorossa Aki Kaurismäen Suomi-trilogian ensimmäinen osa, Kauas pilvet karkaavat (1996).`,
      `Helsinki-viikkoa voi viettää myös kotikulmilla.`,
      `Ohjelmaa järjestetään viikon aikana lähes kaikissa kaupunginosissa ja erityisesti lapsilleja nuorille on runsaasti ohjelmaa.`,
      `Festivaalin koko ohjelma on internetissä.`,
    ],

    sourcePhrases: [
      `The program from morning to night`,
      `Helsinki Week starts today`,
      `This year, the traditional Helsinki Day will be celebrated for a whole week.`,
      `The organisers of the event want people to be able to join in easily, for example during a shopping trip or business trip.`,
      `Therefore, the program has a lot of outdoor events in the middle of the city.`,
      `Today, Saturday, the start day of the festival, has the fullest program.`,
      `The festivities will begin at Senate Square at 12 noon, when the mayor will give a speech and Helsinki City Orchestra will give a gala concert.`,
      `The steps of the cathedral are reserved for the public, as many spectators are expected to attend the event.`,
      `Senate Square also serves 19th-century café delicacies in a cozy old-fashioned market café.`,
      `There is a lot going on in the city center during the day: you can learn parity dances at Rautatientori and a beach volleyball city cup will be played on the shores of Hietaniemi, where anyone can participate.`,
      `Esplanade Park will focus on culture: poems will be recited at the Runeberg statue, improvisational theatre will be performed on the Espa stage, and passersby can also write their Helsinki-themed memories in a giant book.`,
      `The book will be published in the autumn under the name My Helsinki.`,
      `At 10 pm, the Senate Square stage will turn into a movie scene.`,
      `One Helsinki-themed film will be shown there every night.`,
      `Today it is the turn of the first part of Aki Kaurismäki's Finland trilogy, Far Away Clouds (1996).`,
      `Helsinki Week can also be spent at home.`,
      `The program will be held during the week in almost all districts and there is plenty in the program for children and young people.`,
      `The entire festival program is online.`,
    ],
  };
</script>

<Flashcards {...content} />
