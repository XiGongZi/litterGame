<template>
  <div class="coordinate-circle-render">
  </div>
</template>
<script>
export default {
  name: 'coordinate-circle-render',
  components: {},
  data() {
    return {};
  },
  props: {
    circleInfo: {
      type: Object,
      default() {
        return {
          coords: [0, 0]
        };
      }
    }
  },
  computed: {},
  created() {},
  mounted() {},
  watch: {},
  methods: {}
};
</script>
<style lang="less" scoped>
.coordinate-circle-render {
  background:#000;
  width:100px;
  height:100px;
}
</style>
