<template>
  <div v-cloak v-if="links" class="container-fluid">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="container">
        <div class="navbar-brand">
          <a
            role="button"
            aria-label="menu"
            aria-expanded="false"
            class="navbar-burger"
            :class="{ 'is-active': showMenu }"
            @click="$emit('navbar-toggle')"
          >
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
          </a>
        </div>
        <div class="navbar-menu" :class="{ 'is-active': showMenu }">
          <div class="navbar-start">
            <a
              v-for="(link, key) in links"
              :key="key"
              class="navbar-item"
              rel="noreferrer"
              :href="link.url"
              :target="link.target"
            >
              <i v-if="link.icon" :class="['fa-fw', link.icon]"></i>
              {{ link.name }}
            </a>
          </div>
          <div class="navbar-end">
            <slot></slot>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    open: {
      type: Boolean,
      default: false,
    },
    links: Array,
  },
  emits: ["navbar-toggle"],
  computed: {
    showMenu: function () {
      return this.open && this.isSmallScreen();
    },
  },
  methods: {
    isSmallScreen: function () {
      return window.matchMedia("screen and (max-width: 1023px)").matches;
    },
  },
};
</script>

<style lang="scss" scoped>
@media (min-width: 1023px) {
  i.fa-fw {
    width: 0.8em;
  }
}
</style>
