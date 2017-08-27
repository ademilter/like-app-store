<template>
  <div class="detail">
    <div class="container">
      <button type="button" class="fs" @click="enterFullScreen">Open More Detail</button>
      <div class="card">
        <button type="button" class="cl" @click="exitFullScreen">back</button>
      </div>
      <figure>
        <img :src="detail.cover_photo"/>
      </figure>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Detail',
    props: ['detail'],
    data () {
      return {
        init_styles: {}
      }
    },
    methods: {
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

        $el.style.left = this.init_styles.left + 'px'
        $el.style.top = this.init_styles.top + 'px'
        $el.style.width = this.init_styles.width + 'px'
        $el.style.height = this.init_styles.height + 'px'

        const listener = () => {
          let $allShadowEl = document.querySelector('.shadow-detail')
          $el.parentNode.removeChild($allShadowEl)

          $el.style = ''
          $el.classList.remove('done-fullScreen')

          document.querySelector('body').style.overflow = ''
          $el.removeEventListener(whichTransitionEvent, listener)
        }

        $el.addEventListener(whichTransitionEvent, listener)
      },
      enterFullScreen () {
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
          $newEl.classList.add('shadow-detail')
          $newEl.style.height = elHeight + 'px'
          $el.parentNode.insertBefore($newEl, $el)

          $el.classList.add('done-fullScreen')

          $el.style.left = 0
          $el.style.top = 0
          $el.style.width = '100%'
          $el.style.height = '100%'

          document.querySelector('body').style.overflow = 'hidden'
        }, 20)
      }
    }
  }
</script>

<style lang="scss">

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
