<template>
  <q-layout>
    <div style="height: 50px">
      <q-toolbar
        class="flex flex-center"
        :class="pageScroll ? 'dragNav' : 'normalNav'"
      >
        <div class="row items-center full-width" style="max-width: 1200px">
          <q-toolbar-title> Blog </q-toolbar-title>
          <q-space></q-space>
          <div
            class="q-mx-sm cursor-pointer"
            v-for="(menu, mIdx) in essentialLinks"
            :key="mIdx"
            @click="menu.anchor ? openPage(menu.link) : $router.push(menu.link)"
          >
            {{ menu.title }}
          </div>
          <q-btn
            flat
            dense
            round
            icon="menu"
            aria-label="Menu"
            class="cursor-pointer xl-hide lg-hide"
            @click="toggleLeftDrawer"
          />
        </div>
      </q-toolbar>
    </div>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { computed, onMounted, ref, watch } from 'vue';
import EssentialLink, {
  EssentialLinkProps,
} from 'components/EssentialLink.vue';

const pageScroll = ref(false);
const scrollThrottle = ref(false);

const essentialLinks: EssentialLinkProps[] = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev',
    anchor: false,
  },
  {
    title: 'Career',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev',
    anchor: false,
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/dofoong',
    anchor: true,
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

function genDragHeight() {
  if (!scrollThrottle.value) {
    scrollThrottle.value = true;
    if (window.scrollY > 50) {
      pageScroll.value = true;
    } else {
      pageScroll.value = false;
    }

    setTimeout(() => {
      scrollThrottle.value = false;
    }, 10);
  }
}

function openPage(href: string) {
  window.open(href, '_blank');
}

onMounted(() => {
  document.addEventListener('scroll', genDragHeight);
});
</script>
<style lang="scss" scoped>
.dragNav {
  position: fixed;
  top: 0px;
  border-bottom: 1px solid rgba(73, 73, 73, 0.363);
  background-color: white;
  // background-color: rgb(54, 51, 51);
  // color: white;
  z-index: 999;
}
</style>
