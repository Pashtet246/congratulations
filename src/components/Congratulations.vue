<template>
<div class="main">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
  <Header/>

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

  <Pagination/>
</div>

  
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator'
import Header from './Header/Header.vue'
import Pagination from './Pagination/Pagination.vue'

@Component({
  components: {
    Header,
    Pagination
  }
})

export default class happyBirthday extends Vue {

  get contentList() {
    return this.$store.getters.getContentList
  }
  
  get currentPage() {
    return 1
  }

  };
</script>

<style lang="scss">
  @import 'styles';
</style>
