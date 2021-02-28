<template>
    <div ref="fitElement">
        <slot></slot>
    </div>
</template>

<script>
import textFit from '../textfit'

export default {
  name: 'TextFit',
  props: {
      width: {
          type: Number,
          default: 0,
      },
      height: {
          type: Number,
          default: 0,
      },
      multiLine: {
          type: Boolean,
          default: false
      },
      minFontSize: {
          type: Number,
          default: 20,
      },
      maxFontSize: {
          type: Number,
          default: 80,
      },
      detectMultiLine: {
          type: Boolean,
          default: false,
      }},
  data () {
    return {
      fontSize: '0px',
    }},
  mounted() {
    console.log('<TextFit> calling doTextFit from mounted()')
    this.doTextFit()
  },
  updated() {
    console.log('<TextFit> calling doTextFit from updated()')
    this.doTextFit()
  },

  methods: {
      doTextFit() {
          let el = this.$refs.fitElement
          let width = el.clientWidth
          let height = el.clientHeight
          if (this.$props.width) {
            width = this.$props.width
          }
          if (this.$props.height) {
            height = this.$props.height
          }
          this.$nextTick(() =>
            textFit(el, {
                width: width,
                height: height,
                minFontSize: this.$props.minFontSize,
                maxFontSize: this.$props.maxFontSize,
                multiLine: this.$props.multiLine,
                detectMultiLine: this.$props.detectMultiLine,
            }))
      }
  }
}
</script>

<style scoped>
</style>
