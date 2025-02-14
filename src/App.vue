<template>
  <Bar />
  <main>
    <AppMenu />
    <router-view />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Bar from '@/components/Bar.vue'
import AppMenu from '@/components/Menu.vue'

export default defineComponent({
  components: {
    Bar,
    AppMenu,
  },
})
</script>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
}
</style>
