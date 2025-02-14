<template>
  <div class="container">
    <router-link :key="page.name" v-for="page in pages" :to="page.link">
      {{ page.name }}
    </router-link>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      pages: [
        {
          name: 'Podsumowanie',
          link: '/',
        },
        {
          name: 'Plan Zajęć',
          link: '/',
        },
        {
          name: 'Oceny',
          link: '/',
        },
        {
          name: 'Sprawdziany',
          link: '/',
        },
        {
          name: 'Kalendarz',
          link: '/',
        },
      ],
    }
  },
})
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;

  a {
    display: inline-flex;
    background: $dark;
    // margin: 5px 10px;
    justify-content: center;
    align-items: center;
    padding: 5px 10px;
    flex-grow: 1;
    transition: all 0.2s;
    &:hover {
      background: $dark_gray;
    }
  }
}
</style>
