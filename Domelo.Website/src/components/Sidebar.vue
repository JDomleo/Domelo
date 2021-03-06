<template>
  <div>
    <aside class="sidebar" :class="isSidebarOpen ? 'sidebar--open' : false">
      <div class="sidebar__container">
        <div class="sidebar__header">
          <router-link class="sidebar__header-link" to="/">
            <h2 class="sidebar__header-title">Domelo</h2>
          </router-link>
          <p>A design system by <a href="https://jackdomleo.dev" target="_blank">Jack Domleo</a></p>
        </div>
        <button class="button button--cta" @click="toggleTheme">Toggle theme</button>
        <nav class="sidebar__navigation">
          <ul role="tree">
            <li>
              <router-link :to="{ name: Routes.Home }">Home</router-link>
            </li>
            <li>
              Foundation
              <ul role="group">
                <li>
                  <router-link :to="{ name: Routes.FoundationColor }">Color</router-link>
                </li>
                <li>
                  <router-link :to="{ name: Routes.FoundationDesignTokens }">Design tokens</router-link>
                </li>
                <li>
                  <router-link :to="{ name: Routes.FoundationTypography }">Typography</router-link>
                </li>
                <li>
                  <router-link :to="{ name: Routes.FoundationPlatformScale }">Platform scale</router-link>
                </li>
                <li>
                  <router-link :to="{ name: Routes.FoundationObjectStyles }">Object styles</router-link>
                </li>
                <li>
                  <router-link :to="{ name: Routes.FoundationResetStylesheet }">Reset stylesheet</router-link>
                </li>
                <li>
                  <router-link :to="{ name: Routes.FoundationGrid }">Grid</router-link>
                </li>
              </ul>
            </li>
            <li>
              Components
              <ul role="group">
                <li>
                  <router-link :to="{ name: Routes.ComponentsButtons }">Buttons</router-link>
                </li>
              </ul>
            </li>
          </ul>
        </nav>
      </div>
    </aside>
    <div v-if="isSidebarOpen" class="sidebar__overlay" @click="toggleSidebar"></div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator';
import { Routes } from '@/router';

@Component
export default class SideNavigation extends Vue {
  private Routes: Routes = Routes;
  private isSidebarOpen: boolean = false;

  @Prop({ type: Boolean, default: false }) private readonly sidebarOpen!: boolean;

  @Watch('sidebarOpen')
  private onSidebarOpenChanged() {
    this.isSidebarOpen = this.sidebarOpen;
  }

  private toggleSidebar() {
    this.isSidebarOpen = !this.isSidebarOpen;
  }

  private created() {
    this.isSidebarOpen = this.sidebarOpen;
  }

  private toggleTheme() {
    const html = document.getElementById('html');
    const darkTheme = 'theme--dark';
    if (html) {
      if (html.classList.contains(darkTheme)) {
        html.classList.remove(darkTheme);
      } else {
        html.classList.add(darkTheme);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.sidebar {
  background-color: var(--alternate-background-high-color);
  bottom: 0;
  left: auto;
  position: fixed;
  right: 100%;
  top: 0;
  transform: translateX(0);
  transition: var(--transition-timing) transform ease-in-out;
  width: 16rem;
  z-index: 100;

  @media (min-width: 961px) {
    left: 0;
    transform: none;
    transition: none;
  }

  &.sidebar--open {
    @media (max-width: 960px) {
      transform: translateX(100%);
    }
  }

  &__container {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  &__header {
    padding: 0 3rem;
    text-align: center;

    &-link {
      display: block;
      text-decoration-line: none;
    }

    &-title {
      font-size: var(--font-size-800);
    }
  }

  &__navigation {
    flex: 1;
    overflow-x: hidden;
    overflow-y: auto;
  }

  &__overlay {
    background-color: rgba(0, 0, 0, 0.4);
    height: 100vh;
    left: 0;
    position: fixed;
    top: 0;
    width: 100vw;
    z-index: 99;
  }
}
</style>
