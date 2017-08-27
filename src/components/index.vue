<template>
  <div class="details">
    <img src="../assets/ahmed-saffu-208365.jpg"/>
    <Detail v-for="(detail, index) in details"
            :detail="detail"
            :key="index"></Detail>
  </div>
</template>

<script>
  import Detail from './detail'

  export default {
    name: 'Index',
    components: {
      Detail
    },
    data () {
      return {
        details: [
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

  .details {
    padding: 40px;
  }

  .shadow-detail,
  .detail {
    height: 340px;
    margin-bottom: 30px;
  }

</style>
