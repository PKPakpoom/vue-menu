<template>
  <v-app-bar app color="primary">
    <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
    <v-toolbar-title>{{  routeName }}</v-toolbar-title>
  </v-app-bar>
    <v-navigation-drawer
      v-model="drawer"
      temporary
      app
    >



      <v-list density="compact" nav>
        <v-list-item prepend-icon="mdi-home" title="Home" value="home" @click.stop="routeTo('/')"></v-list-item>
        <v-list-item prepend-icon="mdi-store" title="Store" value="store" @click.stop="routeTo('/store')"></v-list-item>
        <v-list-item prepend-icon="mdi-cog" title="Settings" value="settings" @click.stop="routeTo('/settings')"></v-list-item>
      </v-list>
    </v-navigation-drawer>
</template>

<script lang="ts" setup>
  import { ref, computed } from 'vue';
  import { useRouter } from 'vue-router';

  const router = useRouter();
  const drawer = ref(false);
  
  const routeName = computed(() => {
    return router.currentRoute.value.name;
  });

  function routeTo(to: string) {
    drawer.value = false;
    router.push({ "path": to });
  }

</script>
