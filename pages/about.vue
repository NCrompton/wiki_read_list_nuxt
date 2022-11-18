<template>
  <c-flex w="auto" h="2000px" direction="column" ref="container">
    <c-flex w="100%" position="sticky" top="5px" zIndex="2">
      <c-progress :value="progress" m="4" />
    </c-flex>
    <c-grid template-columns="repeat(4, 1fr)">
      <InfoBox v-for="info in infos" v-bind="info" :callback="addSelection" />
    </c-grid>
    <ReadingList :readlist="selection" />
  </c-flex>
</template>
<script lang="js">
import { ref } from 'vue';
import InfoBox from '../components/InfoBox.vue';
import ReadingList from '../components/ReadingList.vue'
export default {
  name: "About",
  components: {
    InfoBox,
    ReadingList,
  },
  inject: ['$chakraColorMode', '$toggleColorMode'],
  setup() {
    const infos = [
      {
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/RybnoeDistrict_06-13_Konstantinovo_Oka_River_04.jpg/330px-RybnoeDistrict_06-13_Konstantinovo_Oka_River_04.jpg",
        place: "Volosovo",
        describe: "The Volosovo culture was discovered in the 1900s. Like other groups with forest origin such as the Garino-Bor and other northern cultures, the Volosovo lived in the forest steppes of the Volga-Ural region, particularly the area of the present-day Samara oblast.",
        kind: "Archeology Site",
        link: "https://en.wikipedia.org/wiki/Volosovo_culture",
      },
      {
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Spit_of_Nizhny_Novgorod_and_Stroganov_Church_at_sunset_01.jpg/405px-Spit_of_Nizhny_Novgorod_and_Stroganov_Church_at_sunset_01.jpg",
        place: "Oka River",
        describe: "The Oka (Russian: Ока́, IPA: [ɐˈka]) is a river in central Russia, the largest right tributary of the Volga. It flows through the regions of Oryol, Tula, Kaluga, Moscow, Ryazan, Vladimir and Nizhny Novgorod and is navigable over a large part of its total length, as far upstream as to the town of Kaluga.",
        kind: "River",
        link: "https://en.wikipedia.org/wiki/Oka_(river)",
      },
      {
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/Pochaev.jpg/488px-Pochaev.jpg",
        place: "Volhynia",
        describe: "Volhynia (also spelled Volynia) (/voʊˈlɪniə/ voh-LIN-ee-ə; Ukrainian: Воли́нь, romanized: Volyn' Polish: Wołyń), is a historic region in Central and Eastern Europe, between south-eastern Poland, south-western Belarus, and western Ukraine.",
        kind: "Historical Region",
        link: "https://en.wikipedia.org/wiki/Volhynia",
      },
      {
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/Manifestaci%C3%B3nAFavorDeLaRep%C3%BAblicaPetrogrado1917--russiainrevolut00jone.jpg/450px-Manifestaci%C3%B3nAFavorDeLaRep%C3%BAblicaPetrogrado1917--russiainrevolut00jone.jpg",
        place: "February Revolution",
        describe: "The February Revolution (Russian: Февра́льская револю́ция, tr. Fevral'skaya revolyutsiya, IPA: [fʲɪvˈralʲskəjə rʲɪvɐˈlʲutsɨjə]), known in Soviet historiography as the February Bourgeois Democratic Revolution[2] and sometimes as the March Revolution,[3] was the first of two revolutions which took place in Russia in 1917.",
        kind: "Event",
        link: "https://en.wikipedia.org/wiki/February_Revolution",
      },
      {
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Mikola_II_%28cropped%29-2.jpg/330px-Mikola_II_%28cropped%29-2.jpg",
        place: "Nicholas II",
        describe: "Nicholas II or Nikolai II Alexandrovich Romanov[d] (18 May [O.S. 6 May] 1868 – 17 July 1918), known in the Russian Orthodox Church as Saint Nicholas the Passion-Bearer,[e] was the last Emperor of Russia, King of Congress Poland and Grand Duke of Finland, ruling from 1 November 1894 until his abdication on 15 March 1917",
        kind: "Historical Figure",
        link: "https://en.wikipedia.org/wiki/Nicholas_II_of_Russia",
      },
    ]
    const progress = ref(0)
    const container = ref(null)
    const selection = ref([])
    return {
      infos,
      progress,
      container,
      selection,
    }
  },
  data() {
    return {
      showModal: false,
      mainStyles: {
        dark: {
          bg: 'gray.700',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'white',
          color: 'gray.900'
        }
      }
    }
  },
  computed: {
    colorMode() {
      return this.$chakraColorMode()
    }
  },
  methods: {
    onScroll(e) {
      this.progress = (window.top.scrollY / (this.$refs.container.$el.clientHeight - window.innerHeight)) * 100
    },
    addSelection(item) {
      this.selection.includes(item) ? (this.selection = this.selection.filter(e => e !== item)) :
        this.selection.push(item)
      console.log(this.selection)
    }
  },
  mounted() {
    window.addEventListener("scroll", this.onScroll)
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.onScroll)
  }
}
</script>
