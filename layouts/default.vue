<template>
  <div class="layout">
    <sidebar />
    <div class="content">
      <nuxt />
    </div>
  </div>
</template>

<script>
import Grid from '~/components/Grid.vue'
import Sidebar from '~/components/Sidebar.vue'
import gsap from "gsap"
import BezierEasing from "bezier-easing"

export default {
  components: { Sidebar, Grid },
  beforeMount: function () {
    gsap.from("body", 2, {opacity: 0, ease: BezierEasing(0.37, -0.04, 0.25, 1)});
  }
}
</script>

<style lang='scss'>
$sidebar-thickness-left: 6rem;

.content {
  position: relative;
  padding-top: $sidebar-thickness-top;
}

html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

html, body, #__nuxt, #__layout {
  height: auto;
}

#__layout {
  position: relative;
  display: flex;
  flex-direction: column;
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
</style>
