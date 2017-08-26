<template>
  <div class="details">

    <div class="detail">
      <div class="container">
        <button type="button" class="fs" @click="fullScreen($event)">Open More Detail</button>
        <div class="card">
          <button type="button" class="cl" @click="close($event)">back</button>
        </div>
        <figure>
          <img src="../assets/ahmed-saffu-208365.jpg"/>
        </figure>
      </div>
    </div>

    <div class="detail">
      <div class="container">
        <button type="button" class="fs" @click="fullScreen($event)">Open More Detail</button>
        <div class="card">
          <button type="button" class="cl" @click="close($event)">back</button>
        </div>
        <figure>
          <img src="../assets/erica-leong-276350.jpg"/>
        </figure>
      </div>
    </div>

    <div class="detail">
      <div class="container">
        <button type="button" class="fs" @click="fullScreen($event)">Open More Detail</button>
        <div class="card">
          <button type="button" class="cl" @click="close($event)">back</button>
        </div>
        <figure>
          <img src="../assets/mona-magnussen-66660.jpg"/>
        </figure>
      </div>
    </div>

    <div class="detail">
      <div class="container">
        <button type="button" class="fs" @click="fullScreen($event)">Open More Detail</button>
        <div class="card">
          <button type="button" class="cl" @click="close($event)">back</button>
        </div>
        <figure>
          <img src="../assets/pacto-visual-157776.jpg"/>
        </figure>
      </div>
    </div>

    <div class="detail">
      <div class="container">
        <button type="button" class="fs" @click="fullScreen($event)">Open More Detail</button>
        <div class="card">
          <button type="button" class="cl" @click="close($event)">back</button>
        </div>
        <figure>
          <img src="../assets/paul-330307.jpg"/>
        </figure>
      </div>
    </div>

  </div>
</template>

<script>
  //  import anime from 'animejs'

  let transEndEventNames = {
    'WebkitTransition': 'webkitTransitionEnd',
    'MozTransition': 'transitionend',
    'transition': 'transitionend'
  }
  let transEndEventName = transEndEventNames[window.Modernizr.prefixed('transition')]

  export default {
    name: 'Index',
    data () {
      return {
        styles: null
      }
    },
    methods: {
      close (event) {
        const $el = event.target.parentNode.parentNode.parentNode
        $el.classList.remove('start-fullScreen')

        const listener = () => {
          let $allShadowEl = document.querySelector('.shadow-detail')
          $el.parentNode.removeChild($allShadowEl)

          $el.style = ''
          $el.classList.remove('done-fullScreen')

          document.querySelector('body').style.overflow = ''
          $el.removeEventListener(transEndEventName, listener)
        }

        $el.addEventListener(transEndEventName, listener)

        $el.style.left = this.styles.left + 'px'
        $el.style.top = this.styles.top + 'px'
        $el.style.width = this.styles.width + 'px'
        $el.style.height = this.styles.height + 'px'
      },

      fullScreen (event) {
        const $el = event.target.parentNode.parentNode
        const rect = $el.getBoundingClientRect()
        const elLeft = rect.left
        const elTop = rect.top
        const elWidth = $el.offsetWidth
        const elHeight = $el.offsetHeight

        this.styles = {
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
          const $newEl = document.createElement('DIV')
          $newEl.classList.add('shadow-detail')
          $newEl.style.height = elHeight + 'px'
          $el.parentNode.insertBefore($newEl, $el)

          document.querySelector('body').style.overflow = 'hidden'

          $el.classList.add('done-fullScreen')

          $el.style.left = 0
          $el.style.top = 0
          $el.style.width = '100%'
          $el.style.height = '100%'
        }, 10)
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

  .detail {
    overflow: hidden;
    border-radius: 15px;
    background-color: #fff;
    box-shadow: 0 10px 30px rgba(black, .2);
    transition: all .7s;
    transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);

    .container {
      position: relative;
      height: 100%;
    }

    &.start-fullScreen {
      border-radius: 0;
      // box-shadow: 0 0 0 rgba(black, 0);
    }

    &.done-fullScreen {
      z-index: 10;
      position: fixed;
    }

    .fs {
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

    &.start-fullScreen {
      .fs {
        display: none;
      }
    }

    .card {
      z-index: 9;
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      max-height: 400px;
    }

    .cl {
      display: none;
    }

    &.start-fullScreen {
      .cl {
        display: block;
      }
    }

    figure {
      overflow: hidden;
      max-height: 400px;
      position: absolute;
      left: -6%;
      top: -6%;
      right: -6%;
      bottom: -6%;
      width: 112%;
      transition: all .7s;
      transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }

    &.start-fullScreen {
      figure {
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        width: 100%;
      }
    }
  }

</style>
