<template lang="pug">
  div(:class='{index}', class='root')
    resize-observer(@notify='setClientWidth', class="hide-print")
    transition(name='fade')
      LayoutHeader(v-if='!index')
    transition(name='fade')
      LayoutNav(v-if='showMenu')
    //- Logo(:invert='index')
    nuxt
</template>

<script>
import { mapActions, mapState } from 'vuex'

export default {
  computed: {
    ...mapState(['view']),
    showMenu () {
      return !this.index && (this.view.showMenu || this.view.width >= 1400)
    },
    index () {
      return this.$route.name === 'index'
    }
  },
  mounted () {
    this.setClientWidth()
  },
  methods: {
    ...mapActions([
      'setClientWidth'
    ])
  }
}
</script>

<style scoped lang="scss">
@import "~@/assets/style/global";
.root {
  @include flex-column();
  align-items: center;
  width: 100%;
  min-height: 100vh;
  // padding: $spacing;
  background: $color-white;
  transition: color $transition-time, background $transition-time;

  @include ie {
    // &.index {
      display: block !important;
    // }
  }

  @include print {
    display: block;
    min-height: none;
  }
}
</style>
