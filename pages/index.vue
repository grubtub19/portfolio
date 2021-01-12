<template>
  <div class="page">
    <github />
  </div>
</template>

<script>
import Github from '~/components/Github.vue'
import gsap from 'gsap'

export default {
  components: {
     Github
  },
  mounted() {
    const timeline = new gsap.timeline();
    timeline.from(".NuxtLogo", {transform: 'translateX(-80vw)', duration: 1, rotation: 500});
  }
}
</script>

<style lang='scss'>
.entry {
  width: 100%;
  section {
    position: relative;
    margin-bottom: 150px;

    img {
      position: relative;
      left: $grid-1;
      width: $grid-10;

      @include sm {
        position: relative;
        left: $grid-4;
        width: $grid-7;
      }
    }

    .desc {
      position: relative;
      top: 0;
      left: $grid-1;
      width: $grid-3;
      font-size: 20px;
      color: $text-color;

      @include sm {
        position: absolute;
        font-size: 30px;
      }

      @include md {
        font-size: 50px;
      }
    }
  }
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
