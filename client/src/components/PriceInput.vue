<template lang="pug">
  Price.price
    span $

    .fake-input
      span.editable( 
        contenteditable
        @keypress="keypress" 
        @input="({ target }) => price = target.textContent" 
        v-once
      ) {{ value }}

      span.placeholder price
</template>

<script>
  import Price from '@/components/Price'

  export default {
    props: {
      value: {
        type: Number,
        default () {
          return 0
        },
      },
    },

    components: {
      Price,
    },

    data () {
      return {
        price: 0,
      }
    },

    methods: {
      keypress (event) {
        if (!/[0-9]/.test(event.key)) {
          event.preventDefault()
          event.stopPropagation()

          return false
        }
      },

      output () {
        this.$emit('input', this.price)
      },
    },

    watch: {
      price () {
        this.output()
      },
    },
  }
</script>

<style lang="sass" scoped>
  .price
    height: 40px
    display: flex
    overflow: hidden
    color: var(--text)
    fill: var(--text)
    display: flex
    align-items: center
    justify-content: center
    width: auto
    padding: 0 10px

    .icon
      width: 40px
      height: 40px
      display: flex
      align-items: center
      justify-content: center

    span
      margin-right: 4px
      font-weight: bold
      font-size: 16px

    .fake-input
      position: relative
      outline: none

      span
        display: block

      span:empty
        min-width: 30px

      span + .placeholder
        pointer-events: none
        position: absolute
        opacity: 0
        top: 0

      span:empty + .placeholder
        opacity: 0.7
    
    input
      flex-grow: 1
      font-weight: bold
      font-size: 16px
</style>
