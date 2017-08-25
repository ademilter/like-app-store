<template>
  <div class="details">

    <div class="detail">
      <div class="container">
        <button type="button" @click="fullScreen($event)">Open More Detail</button>
        <img src="../assets/andrew-pons-57133.jpg"/>
      </div>
    </div>
    <div class="detail">
      <div class="container">
        <button type="button" @click="fullScreen($event)">Open More Detail</button>
        <img src="../assets/eddie-kopp-263580.jpg"/>
      </div>
    </div>
    <div class="detail">
      <div class="container">
        <button type="button" @click="fullScreen($event)">Open More Detail</button>
        <img src="../assets/jacob-hilton-228982.jpg"/>
      </div>
    </div>
    <div class="detail">
      <div class="container">
        <button type="button" @click="fullScreen($event)">Open More Detail</button>
        <img src="../assets/kyaw-tun-263670.jpg"/>
      </div>
    </div>

  </div>
</template>

<script>
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
        el: null
      }
    },
    methods: {
      fullScreen (event) {
        const $el = event.target.parentNode.parentNode

        if ($el.classList.contains('is-fullScreen')) {
          //
          // EXIT FULL-WIDTH
          //
          let that = this
          const listener = function () {
            console.log('event')
            if (that.el) {
              $el.parentNode.removeChild(that.el)
              that.el = null
            }
            //
            $el.style = ''
            $el.classList.remove('is-fullScreen')
            //
            document.querySelector('body').style.overflow = ''
            $el.removeEventListener(transEndEventName, listener)
          }
          $el.addEventListener(transEndEventName, listener)
          //
          const VAL = JSON.parse(localStorage.verahu)
          //
          $el.style.left = VAL.left + 'px'
          $el.style.top = VAL.top + 'px'
          $el.style.width = VAL.width + 'px'
          $el.style.height = VAL.height + 'px'
          //
        } else {
          //
          // ENTER FULL-WIDTH
          //
          const rect = $el.getBoundingClientRect()
          const elLeft = rect.left
          const elTop = rect.top
          const elWidth = $el.offsetWidth
          const elHeight = $el.offsetHeight

          localStorage.verahu = JSON.stringify({
            left: elLeft,
            top: elTop,
            width: elWidth,
            height: elHeight
          })

          $el.style.left = elLeft + 'px'
          $el.style.top = elTop + 'px'
          $el.style.width = elWidth + 'px'
          $el.style.height = elHeight + 'px'
          //
          setTimeout(() => {
            const $newEl = document.createElement('DIV')
            $newEl.classList.add('detail')
            $newEl.style.height = elHeight + 'px'
            $el.parentNode.insertBefore($newEl, $el)
            this.el = $newEl
            //
            document.querySelector('body').style.overflow = 'hidden'
            //
            $el.classList.add('is-fullScreen')
            $el.style.left = 0
            $el.style.top = 0
            $el.style.width = '100%'
            $el.style.height = '100%'
          }, 10)
        }
      }
    }
  }
</script>

<style lang="scss">

  .details {
    padding: 40px;
  }

  .detail {
    margin-bottom: 30px;
    transition: all .3s;
    background-color: #000;

    .container {
      position: relative;
      height: 300px;
      overflow: hidden;
    }

    &.is-fullScreen {
      z-index: 10;
      position: fixed;

      .container {
        height: 100%;
      }
    }

    button {
      z-index: 9;
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

    img {
      width: 100%;
    }
  }

</style>
