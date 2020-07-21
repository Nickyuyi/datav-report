<template>
  <div class="home">
    <top-view />
    <sales-view />
    <bottom-view />
  </div>
</template>

<script>
import TopView from '../components/TopView'
import SalesView from '../components/SalesView'
import BottomView from '../components/BottomView'
import { wordcloud, screenData, mapScatter } from '../api'

export default {
  name: 'Home',
  components: {
    TopView,
    SalesView,
    BottomView
  },
  data() {
    return {
      reportData: null,
      wordCloud: null,
      mapData: null
    }
  },
  methods: {
    getReportData() {
      return this.reportData
    },
    getWordCloud() {
      return this.wordCloud
    },
    getMapData() {
      return this.mapData
    }
  },
  provide() {
    return {
      data: this.reportData,
      getReportData: this.getReportData,
      getWordCloud: this.getWordCloud,
      getMapData: this.getMapData
    }
  },
  mounted() {
    screenData().then(data => { this.reportData = data })
    wordcloud().then(data => { this.wordCloud = data })
    mapScatter().then(data => { this.mapData = data })
  }
}
</script>

<style lang="scss" scoped>
  .home {
    width: 100%;
    padding: 20px;
    background: #eee;
    box-sizing: border-box;
  }
</style>
