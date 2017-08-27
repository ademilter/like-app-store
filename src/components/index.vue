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
            cover_photo: 'ahmed-saffu-208365.jpg',
            title: 'asdasd'
          },
          {
            cover_photo: 'erica-leong-276350.jpg',
            title: 'asdasd'
          },
          {
            cover_photo: 'mona-magnussen-66660.jpg',
            title: 'asdasd'
          },
          {
            cover_photo: 'pacto-visual-157776.jpg',
            title: 'asdasd'
          },
          {
            cover_photo: 'paul-330307.jpg',
            title: 'asdasd'
          }
        ]
      }
    }
  }
</script>

<style lang="scss">

  .Cards {
    padding: 40px;
  }

  .shadow-Card,
  .Card {
    height: 340px;
    margin-bottom: 30px;
  }

</style>
