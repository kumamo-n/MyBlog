<template>
  <div id="app">
    <Header :class="{ shrink: !headerHide }" />
    {{ this.headerHide }}
    <main id="wrap">
      <nuxt />
    </main>
    <Footer />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { scroll } from "@/lib/scroller";
const Header = () => import("@/containers/Header.vue");
const Footer = () => import("@/containers/Footer.vue");
export default Vue.extend({
  components: {
    Footer,
    Header,
  },
  data() {
    return {
      headerHide: true,
    };
  },
  mounted() {
    if (window) {
      window.addEventListener("scroll", this.scrollEvent);
    }
  },
  methods: {
    scrollEvent() {
      const scrollEvent = scroll(document.scrollingElement, 700);
      if (scrollEvent) {
        this.headerHide = false;
      } else {
        this.headerHide = true;
      }
    },
  },
});
</script>

<style lang="scss">
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

#wrap {
  margin-top: 140px;
}
.shrink {
  transform: translateY(-100%);
}
@media screen and (max-width: 768px) {
  #wrap {
    margin-top: 100px;
  }
}
</style>
