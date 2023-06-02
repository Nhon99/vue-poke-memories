<template>
  <main-screen v-if="isPlay==='default'" @onPlay="handlePlay($event)"/>
  <interact-screen v-if="isPlay==='match'" @onFinish="handleResult" :cardList="settings.cardList"/>
  <result-screen v-if="isPlay==='result'" @onStartAgain="isPlay='default'" :timePlay="timePlay"/>
  <coppy-screen/>
</template>

<script>
import CoppyScreen from './components/CoppyRightScreen.vue'
import MainScreen from './components/MainScreen.vue'
import InteractScreen from './components/InteractScreen.vue'
import ResultScreen from './components/ResultScreen.vue'

import { shuffled } from './utils/Array.js'

export default {
  name: 'App',
  components: {
      CoppyScreen,
      MainScreen,
      InteractScreen,
      ResultScreen
  },
  data () {
      return {
          settings : {
              totalOfCard:0,
              cardList:[],
              statusAt: null,
          },
          isPlay: 'default',
          timePlay: 0
      }
  },
  methods: {
      handlePlay (config) {
          console.log('running....', config)
          this.settings.totalOfCard = config.totalBlock
          const firstCards = Array.from({length: this.settings.totalOfCard / 2}, (_, i) => i+1)
          const secondCards = [...firstCards]
          const cards = [...firstCards,...secondCards]
          this.settings.cardList =  shuffled(shuffled(shuffled(shuffled(cards))))

          this.settings.statusAt = new Date().getTime()

          console.log('time',this.settings.statusAt)
          
          console.log(this.settings.cardList)

          this.isPlay = 'match'
      },
      handleResult() {
          //Tinh thoi gian choi
          this.timePlay = Math.round((new Date().getTime() - this.settings.statusAt)/1000)
          console.log(this.timePlay)
          //chuyen sang man result
          this.isPlay = 'result'
      }
  }
}
</script>
