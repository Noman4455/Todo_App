<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-img class="img" src="~assets/mountains.jpg">
        <q-toolbar class="bg-transparent">
          <q-btn
            flat
            dense
            icon="menu"
            aria-label="Menu"
            @click="leftDrawerOpen = !leftDrawerOpen"
          />
        </q-toolbar>
      </q-img>
      <div class="bg-transparent text-white absolute-bottom q-pl-lg q-mb-lg">
        <div class="text-h5 text-weight-bold">Todo List</div>
        <div>{{ todaysDate }}</div>
      </div>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="250"
      :breakpoint="700"
    >
      <q-scroll-area
        style="
          height: calc(100% - 200px);
          margin-top: 200px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item clickable v-ripple to="/" exact>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> TODO </q-item-section>
          </q-item>
          <q-item clickable v-ripple to="/help" exact>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="~assets/mountains.jpg"
        style="height: 200px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="~assets/My.jpeg" />
          </q-avatar>
          <div class="text-weight-bold">M. Noman Tariq</div>
          <div>@PowerSoft</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
      <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from "quasar";

export default {
  name: "MainLayout",

  data() {
    return {
      leftDrawerOpen: false,
    };
  },
  computed: {
    todaysDate() {
      const timeStamp = Date.now();
      return date.formatDate(timeStamp, "dddd DD MMMM");
    },
  },
};
</script>


<style>
.img {
  height: 200px;
  filter: grayscale(100%);
  opacity: 0.5;
}
</style>
