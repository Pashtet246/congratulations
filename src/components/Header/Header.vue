<template>
  <header>
    <div class="mainHeader">
      <div class="backButton">
        <i class="material-icons white">arrow_back</i>
      </div>
      <div class="grats">
        <span>Поздравление Дмитрию с днём рождения </span>
      </div>
      <div class="helpIcon">
        <i class="material-icons white">help</i>
      </div>
    </div>
    <div class="subHeader">
      <ul class="nav">
        <li class="helpIcon" v-if="showMore">
          <i class="material-icons white"
              @click="showMore = false">chevron_left</i>
        </li>
        <li class="nav__item"
            v-for="(item, index) in headerItems"
            :key="index"
            :class="{'nav__item--current': activeIndex === index}"
            @click="changeTab(index)">
          {{item.name.toUpperCase()}}
        </li>
        <li class="helpIcon" v-if="!showMore">
          <i class="material-icons white"
              @click="showMore = true">chevron_right</i>
        </li>
      </ul>
    </div>
  </header>
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator'

@Component

export default class header extends Vue {
  activeIndex: number = 0
  firstItem: number = 0
  showMore: boolean = false

  get countItems () {
    if (window.innerWidth >= 500) {
      return 5
    } else {
      return window.innerWidth/100
    }
  }

  get headerItems() {
    if ( this.showMore === true && this.countItems < this.$store.getters.getItems.length + 1) {
      return this.$store.getters.getItems.slice(this.countItems, (this.$store.getters.getItems.length + 1))
    } else {
      return this.$store.getters.getItems.slice(0, this.countItems)
    }
  }

  get activeComponent() {
    return this.$store.getters.getItems[this.activeIndex]
  }

  @Emit('change')
    changeTab(index: number) {
      this.activeIndex = index
    }
  }

</script>

<style lang="scss" scoped>
  @import 'styles';
</style>