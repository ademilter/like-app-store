<template>
  <div class="Card" :class="'Card--' + Card.theme">
    <div class="Card-container">

      <button type="button" class="Card-fullScreen"
              @click="enterFullScreen">Open More Detail
      </button>

      <div class="Card-info">

        <figure class="Card-info-cover">
          <img :src="getImgUrl()"/>
        </figure>

        <button type="button" class="Card-info-close"
                @click="exitFullScreen">
          <svg xmlns="http://www.w3.org/2000/svg" width="78" height="78" viewBox="0 0 78 78">
            <g fill="#fff">
              <path
                d="M39,77.5 C60.2,77.5 77.5,60.2 77.5,39 C77.5,17.8 60.2,0.5 39,0.5 C17.8,0.5 0.5,17.8 0.5,39 C0.5,60.2 17.8,77.5 39,77.5 Z M39,5.5 C57.5,5.5 72.5,20.5 72.5,39 C72.5,57.5 57.5,72.5 39,72.5 C20.5,72.5 5.5,57.5 5.5,39 C5.5,20.5 20.5,5.5 39,5.5 Z"/>
              <path
                d="M25.2,52.8 C25.7,53.3 26.3,53.5 27,53.5 C27.7,53.5 28.3,53.3 28.8,52.8 L39,42.5 L49.3,52.8 C49.8,53.3 50.4,53.5 51.1,53.5 C51.8,53.5 52.4,53.3 52.9,52.8 C53.9,51.8 53.9,50.2 52.9,49.3 L42.5,39 L52.8,28.7 C53.8,27.7 53.8,26.1 52.8,25.2 C51.8,24.2 50.2,24.2 49.3,25.2 L39,35.5 L28.7,25.2 C27.7,24.2 26.1,24.2 25.2,25.2 C24.2,26.2 24.2,27.8 25.2,28.7 L35.5,39 L25.2,49.3 C24.2,50.2 24.2,51.8 25.2,52.8 Z"/>
            </g>
          </svg>


        </button>

        <h2 class="Card-info-title">{{ Card.title }}</h2>

        <div class="Card-info-bar">
          <div class="Card-info-bar-info">
            <h5>Old Man's Journey</h5>
            <h6>Bulmaca</h6>
          </div>
          <div class="Card-info-bar-purchase">
            <button type="button">17,99 TL</button>
          </div>
        </div>

      </div>

      <div class="Card-body">
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit.
          Adipisci consequatur deleniti ducimus quas similique?
          Consectetur odit sed suscipit tempora.
          Dolore, eaque et ipsa maxime minus officia provident sapiente unde voluptatum.
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit.
          Adipisci consequatur deleniti ducimus quas similique?
          Consectetur odit sed suscipit tempora.
          Dolore, eaque et ipsa maxime minus officia provident sapiente unde voluptatum.
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit.
          Adipisci consequatur deleniti ducimus quas similique?
          Consectetur odit sed suscipit tempora.
          Dolore, eaque et ipsa maxime minus officia provident sapiente unde voluptatum.
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit.
          Adipisci consequatur deleniti ducimus quas similique?
          Consectetur odit sed suscipit tempora.
          Dolore, eaque et ipsa maxime minus officia provident sapiente unde voluptatum.
        </p>
      </div>

    </div>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: ['Card'],
    data () {
      return {
        init_styles: {}
      }
    },
    methods: {
      getImgUrl () {
        // Fixed: dinamic image path
        let images = require.context('../assets/')
        return images('./' + this.Card.cover_photo)
      },
      whichTransitionEvent () {
        // https://davidwalsh.name/css-animation-callback
        let t
        let el = document.createElement('fake-element')
        let transitions = {
          'transition': 'transitionend',
          'OTransition': 'oTransitionEnd',
          'MozTransition': 'transitionend',
          'WebkitTransition': 'webkitTransitionEnd'
        }
        for (t in transitions) {
          if (el.style[t] !== undefined) {
            return transitions[t]
          }
        }
      },
      exitFullScreen () {
        let whichTransitionEvent = this.whichTransitionEvent()
        let $el = this.$el
        $el.classList.remove('start-fullScreen')
        $el.classList.remove('enter-fullScreen')

        $el.style.left = this.init_styles.left + 'px'
        $el.style.top = this.init_styles.top + 'px'
        $el.style.width = this.init_styles.width + 'px'
        $el.style.height = this.init_styles.height + 'px'

        const listener = () => {
          let $allShadowEl = document.querySelector('.shadow-Card')
          $el.parentNode.removeChild($allShadowEl)

          $el.style = ''
          $el.classList.remove('process-fullScreen')

          document.querySelector('body').style.overflow = ''
          $el.removeEventListener(whichTransitionEvent, listener)
        }

        $el.addEventListener(whichTransitionEvent, listener)
      },
      enterFullScreen () {
        let whichTransitionEvent = this.whichTransitionEvent()
        let $el = this.$el
        let rect = $el.getBoundingClientRect()
        let elLeft = rect.left
        let elTop = rect.top
        let elWidth = $el.offsetWidth
        let elHeight = $el.offsetHeight

        this.init_styles = {
          left: elLeft,
          top: elTop,
          width: elWidth,
          height: elHeight
        }

        $el.classList.add('start-fullScreen')

        $el.style.left = elLeft + 'px'
        $el.style.top = elTop + 'px'
        $el.style.width = elWidth + 'px'
        $el.style.height = elHeight + 'px'

        setTimeout(() => {
          let $newEl = document.createElement('DIV')
          $newEl.classList.add('shadow-Card')
          $newEl.style.height = elHeight + 'px'
          $el.parentNode.insertBefore($newEl, $el)

          $el.classList.add('process-fullScreen')

          $el.style.left = 0
          $el.style.top = 0
          $el.style.width = '100%'
          $el.style.height = '100%'

          document.querySelector('body').style.overflow = 'hidden'
        }, 20)

        const listener = () => {
          $el.classList.add('enter-fullScreen')
          $el.removeEventListener(whichTransitionEvent, listener)
        }
        $el.addEventListener(whichTransitionEvent, listener)
      }
    }
  }
</script>

<style lang="scss">

  .Card {
    $Card: &;
    overflow: hidden;
    border-radius: 15px;
    background-color: #fff;
    box-shadow: 0 10px 30px rgba(black, .2);
    transition: all .7s;
    transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);

    &-container {
      position: relative;
      height: 100%;
    }

    &-fullScreen {
      z-index: 10;
      position: absolute;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
      opacity: 0;
      display: block;
      width: 100%;
      border: 0;
    }

    // INFO

    &-info {
      z-index: 9;
      overflow: hidden;
      position: relative;
      height: 100%;
      max-height: 400px;

      .Card--dark & {
        color: white;
      }
      .Card--light & {

      }

      &-cover {
        z-index: -1;
        position: absolute;
        left: -6%;
        top: -6%;
        right: -6%;
        bottom: -6%;
        width: 112%;
        transition: all .7s;
        transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
      }

      &-close {
        position: absolute;
        right: 20px;
        top: 20px;
        display: none;

        svg {
          font-size: 30px;
          width: 1em;
          height: 1em;
        }
      }

      &-title {
        font-size: 40px;
        position: absolute;
        left: 20px;
        top: 40px;
      }

      &-bar {
        position: absolute;
        left: 20px;
        right: 20px;
        bottom: 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;

        &-purchase {
          button {
            padding: 5px 10px;
            font-weight: bold;
            background-color: #fff;
            color: dodgerblue;
            border-radius: 999px;
          }
        }
      }
    }

    &-body {
      padding: 30px;

      p {
        margin-bottom: 1em;
      }
    }

    &.start-fullScreen {
      z-index: 10;
      border-radius: 0;

      #{$Card}-fullScreen {
        display: none;
      }

      #{$Card}-info {
        &-cover {
          left: 0;
          top: 0;
          right: 0;
          bottom: 0;
          width: 100%;
        }
      }

    }

    &.process-fullScreen {
      z-index: 10;
      position: fixed;
      overflow: auto;
    }

    &.enter-fullScreen {
      #{$Card}-info {
        &-close {
          display: flex;
        }
      }
    }

  }

</style>
