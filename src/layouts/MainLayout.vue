<template>
  <q-layout view="hHh Lpr lff">
    <q-header elevated class="bg-white text-dark" height-hint="98">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="enabledMiniState = !enabledMiniState"
        />
        <q-toolbar-title> Logo </q-toolbar-title>
        <q-btn
          flat
          @click="drawerRight = !drawerRight"
          round
          dense
          icon="menu"
        />
        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="drawerState"
      show-if-above
      bordered
      :mini="enabledMiniState && miniState"
      @mouseover="enabledMiniState ? (miniState = false) : null"
      @mouseout="enabledMiniState ? (miniState = true) : null"
      :breakpoint="500"
      class="bg-grey-3"
    >
      <q-list>
        <!-- <q-item-label header> Essential Links </q-item-label> -->
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-drawer
      side="right"
      v-model="drawerRight"
      bordered
      :width="60"
      class="bg-grey-3"
    >
      <q-scroll-area class="fit">
        <div class="q-pa-sm">
          <div v-for="n in 10" :key="n">{{ n }}</div>
        </div>
      </q-scroll-area>
    </q-drawer>

    <!-- <q-drawer side="right" v-model="drawerRight2" bordered class="bg-grey-6">
      <q-scroll-area class="fit">
        <div class="q-pa-sm">
          <div v-for="n in 10" :key="n">Hello</div>
        </div>
      </q-scroll-area>
    </q-drawer> -->
  </q-layout>
</template>

<script lang="ts">
import EssentialLink from 'components/EssentialLink.vue';

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev',
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework',
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev',
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev',
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev',
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev',
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev',
  },
];

import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',
  components: {
    EssentialLink,
  },
  setup() {
    const drawerState = ref(false);

    return {
      enabledMiniState: ref(false),
      drawerRight: ref(true),
      // drawerRight2: ref(true),
      miniState: ref(true),
      essentialLinks: linksList,
      drawerState,
      toggleLeftDrawer() {
        drawerState.value = !drawerState.value;
      },
    };
  },
});
</script>
