<script setup>
  import {useI18n} from "vue-i18n";
  import {ref} from "vue";
  import {ConfirmDialog as PvConfirmDialog, Drawer as PvDrawer} from "primevue";

  const { t } = useI18n();
  const drawer = ref(false);
  const toggleDrawer = () => { drawer.value = !drawer.value; }

  const items = [
    { label: 'option.home', to: '/home'},
    { label: 'option.about', to: '/about'}
  ];
</script>

<template>
  <pv-toast/>
  <pv-confirm-dialog/>
  <header class="absolute top-0 left-0 w-full">
    <pv-toolbar class="bg-primary">
      <template #start>
        <pv-button class="p-button-text" icon="pi pi-bars" @click="toggleDrawer"/>
        <h3>ACME Learning Center</h3>
      </template>
      <template #end>
        <div class="flex-column mr-3">
          <pv-button v-for="item in items" :key="item.label" as-child v-slot="slotProps">
            <router-link :to="item.to" :class="slotProps['class']">{{ t(item.label)}}</router-link>
          </pv-button>
        </div>
        <!-- To add when IAM is implemented -->
        <!-- <authentication-section/>-->
        <!-- To add when Language switcher is implemented -->
        <!-- <language-switcher/> -->
      </template>
    </pv-toolbar>
    <pv-drawer v-model="drawer"/>
  </header>
  <main class="mt-7">
    <router-view/>
  </main>
  <!-- To add when Footer is implemented -->
  <!-- <footer-content/> -->
</template>
