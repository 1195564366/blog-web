<template>
  <div id="root" :class="skinClass">
    <Header />
    <Nuxt />
    <BackTop />
  </div>
</template>

<script>
import Header from "@components/Header";
import BackTop from "@components/backTop";
import { Cache, Axios } from "@utils";

export default {
  components: {
    Header,
    BackTop,
  },
  data() {
    return {};
  },
  computed: {
    skinClass() {
      return this.$store.state.blog.skin.class;
    },
  },
  mounted() {
    document.getElementById("root").className = this.skinClass;
    this.getConfig();
  },
  methods: {
    async getConfig() {
      const result = await Axios.get("/web/config");
      this.$store.commit("blog/setTitle", result.title);
    },
  },
};
</script>

<style lang="less">
@import url("~static/less/index.less");
#root {
  transition: background 0.5s;
  background: #f4f4f4;
}
</style>
