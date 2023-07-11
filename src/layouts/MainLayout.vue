<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-tabs align="center">
        <q-route-tab to="/" label="Home" />
        <q-route-tab to="/about" label="About" />
        <q-route-tab to="/contact" label="Contact Us" />
      </q-tabs>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
