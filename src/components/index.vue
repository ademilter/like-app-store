<template>
  <div class="Cards">
    <Card v-for="(Card, Index) in Cards"
          :Card="Card"
          :key="Index"></Card>
  </div>
</template>

<script>
  import Card from './card'

  export default {
    name: 'Index',
    components: {
      Card
    },
    data () {
      return {
        Cards: [
          {
            theme: 'dark',
            cover_photo: 'ahmed-saffu-208365.jpg',
            title: 'GÜNÜN OYUNU'
          },
          {
            theme: 'dark',
            cover_photo: 'erica-leong-276350.jpg',
            title: 'GÜNÜN OLAYI'
          },
          {
            theme: 'dark',
            cover_photo: 'mona-magnussen-66660.jpg',
            title: 'GÜNÜN ARTİSTİ'
          },
          {
            theme: 'dark',
            cover_photo: 'pacto-visual-157776.jpg',
            title: 'GÜNÜN TROLÜ'
          },
          {
            theme: 'light',
            cover_photo: 'paul-330307.jpg',
            title: 'GÜNÜN BABASI'
          }
        ]
      }
    }
  }
</script>

<style lang="scss">

  button, a {
    color: inherit;
    cursor: pointer;
  }

  html {
    line-height: 1.2;
  }

  .Cards {
    padding: 30px;
    max-width: 340px;
    margin: 0 auto;
  }

  .shadow-Card,
  .Card {
    height: 300px;
    margin-bottom: 30px;
  }

</style>
