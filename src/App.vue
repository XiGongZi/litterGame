<template>
  <div id="app">
    <my-random :coordinateRandom="coordinateRandom"/>
    <keep-alive :include="include">
      <!-- 需要缓存的视图组件 -->
      <router-view v-if="$route.meta.keepAlive">
      </router-view>
    </keep-alive>

    <router-view v-if="!$route.meta.keepAlive">
    </router-view>
  </div>
</template>

<script>
import compRandom from './components/coordinate-random/main';
// 引入默认全局css
import './assets/css/default.css' ;
export default {
  name: 'App',
  components: {
    'my-random': compRandom
  },
  data() {
    return {
      include: [],
      coordinateRandom:{
        radious:2,
        timeSet:{
          hide:1000
        },
        // countArr:[1,2,3,5,5,6,7,8,9,9]
        countArr:[1,1,1,1,1,1,1,1,1,1]
      }
    };
  },
  computed: {},
  beforeDestroy() {
    this.$store.commit('updateKeepAliveInclude', []);
  },
  watch: {
    $route(to, from) {
      // 如果 要 to(进入) 的页面是需要 keepAlive 缓存的，把 name push 进 include数组
      if (to.meta.keepAlive) {
        this.include.indexOf(to.name) === -1 && this.include.push(to.name);
      }
      // 如果 要 form(离开) 的页面是 keepAlive缓存的，
      // 再根据 deepth 来判断是前进还是后退
      if (from.meta.keepAlive && to.meta.deepth <= from.meta.deepth) {
        var index = this.include.indexOf(from.name);
        index !== -1 && this.include.splice(index, 1);
      }
      this.$store.commit('updateKeepAliveInclude', this.include);
    }
  },
  methods: {}
};
</script>

<style lang="less">
</style>
