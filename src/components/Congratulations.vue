<template>
<div class="main">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
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

  <div class="mainContent">
    <ul class="content">
      <li v-for="(content, index) in contentList"
          :key="index"
          class="contentItem">
          <i class="material-icons blue">play_circle_filled</i>
          <a href="#"> {{content.text}}</a>
      </li>
    </ul>
  </div>

  <div class="pagination">
      <a href="#" class="quotes">&lt;</a>
      <a href="#" class="active">1</a>
      <a href="#">2</a>
      <a href="#">3</a>
      <a href="#" class="breakView">...</a>
      <a href="#">13</a>
      <a href="#">14</a>
      <a href="#">15</a>
      <a href="#" class="quotes">&gt;</a>
  </div>
</div>

  
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator'

@Component

export default class happyBirthday extends Vue {
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

  get contentList() {
    return this.$store.getters.getContentList
  }
  
  get currentPage() {
    return 1
  }

  get activeComponent() {
    return this.$store.getters.getItems[this.activeIndex]
  }

  @Emit('change')
    changeTab(index: number) {
      this.activeIndex = index
    }
  };
</script>


<style lang="scss">
  .pagination {
    display: flex;
    background-color: #ededed;
    justify-content: center;
    align-items: center;
    height: 50px;
  }

  .pagination a {
    color: black;
    float: left;
    padding: 4px 10px;
    text-decoration: none;
    border: 1px solid #ddd;
    background-color: white;
    margin: 0 4px;
    border-radius: 5px;
    font-size: 14px;

    &.breakView {
      border: none;
      background-color:#ededed;
    }

    &.quotes {
      font-weight: bold;
      padding: 2px 8px;
    }
  }

  .pagination a.active {
    background-color: #4285F4;
    color: white;
    border-radius: 5px;
  }

  .pagination a:hover:not(.active) {
    background-color: #ddd;
    border-radius: 5px;
  }

  .contentItem {
    height: 80px;
    width: 100%;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    font-size: 13px;
    font-weight: bold;
    text-align: left;
    box-shadow: 0px 3px 6px 1px rgba(0,0,0,0.3);
    text-overflow: ellipsis;
    overflow: hidden;

    &:last-of-type {
      margin-bottom: 0px;
    }
  }

  .contentItem a {
    padding-right: 30px;
  }

  .material-icons.blue { 
    color: #4285F4;
    font-size: 60px;
    padding-left: 15px;
    cursor: pointer;
  }

  .mainHeader {
    font-size: 20px;
    display: flex;
    height: 40px;
    align-items: center;
    padding-top: 10px;
  }

  .backButton {
    padding-left: 10px;
    flex-shrink: 0;
    cursor: pointer;
  }

  .grats {
    display: flex;
    width: max-content;
    flex-grow: 1;
    padding-bottom: 5px;
    padding-left: 10px;
    padding-right: 10px;
  }

  .helpIcon {
    padding-right: 10px;
    flex-shrink: 0;
    cursor: pointer;
  }

  header {
    background-color: #4285F4;
    color: white;
    box-shadow: 0 7px 10px -6px grey;
  }

  li {
    list-style-type: none;
  }

  .mainContent {
    display: flex;
    justify-content: space-between;
    padding: 15px 20px;
  }

  .content {
    list-style-type: none;
    width: 100%;
    padding: 0;
    margin: 0;
  }

  .subHeader {
    display: flex;
    width: 100%;
    font-size: 16px;
  }

  .nav {
    display: flex;
    width: 100%;
    padding-left: 0px;
    margin-bottom: 0px;
    margin-top: 5px;
  }

  .nav__item {
    display: flex;
    align-items: center;
    height: 28px;
    transition: all ease 0.2s;
    cursor: pointer;
    width: max-content;
    opacity: 0.5;
    font-size: 11px;
    font-weight: bold;
    line-height: 1.5;
    padding-left: 10px;
    width: max-content;
    padding-right: 9px;

    &--current {
      border-right: 1px solid white;
      border-bottom: 2px solid yellow;
      opacity: 1;
    }
  }

  @media (min-width: 600px) {
    .content {
      columns: 2; 
      -moz-columns: 2; 
      -webkit-columns: 2;
    }

    .mainHeader {
      font-size: 20px;
      display: flex;
      height: 40px;
      align-items: center;
      padding-top: 10px;
    }

    .nav__item {
      font-size: 14px;
      padding-left: 30px;
      padding-right: 12px;
      &--current {
        padding-left: 10px;
      }
    }
  }
</style>
