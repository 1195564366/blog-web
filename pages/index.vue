<template>
  <!-- 首页 -->
  <div class="home-wrap">
    <!-- 顶部banner区域 start -->
    <div class="banner-wrap" style="background-image: url(https://ncdn.camarts.cn/dabe33ef.jpg)">
      <img
        class="banner-avatar"
        src="https://www.sanghangning.cn/assets/img/index-logo.acd896b1.gif"
        alt
        @click="goAdmin"
      />
      <div class="banner-right">
        <div class="banner-title">说说我的生活</div>
        <div class="banner-desc">Don't cry, do laugh</div>
      </div>
    </div>
    <!-- 顶部banner区域 end -->
    <div class="main-wrap">
      <articleItem v-for="item in articleList" :key="item.articleId" :article="item" />
    </div>
    <div class="no-more">我也是有底线的~</div>
  </div>
</template>

<script>
import { Axios } from "@utils";
import articleItem from "@components/articleItem";

export default {
  components: {
    articleItem,
  },
  async asyncData({ app }) {
    const [config, articleList] = await Promise.all([
      Axios.get("/web/config"),
      Axios.get("/web/article/list"),
    ]);
    app.head.title = config.title;
    app.head.meta = [
      ...app.head.meta,
      ...[
        { name: "description", content: config.description },
        { name: "keywords", content: config.keywords },
      ],
    ];
    return {
      articleList,
    };
  },
  methods: {
    goAdmin() {
      window.open("/admin/login", "_blank");
    },
  },
};
</script>

<style lang="less" scoped>
@media screen and (max-width: 720px) {
  .banner-avatar {
    display: none;
  }
}
.banner {
  &-wrap {
    // width: 100vw;
    height: 600px;
    background-repeat: no-repeat;
    background-position: 50%;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #ffffff;
  }
  &-avatar {
    width: 7rem;
    margin-right: 40px;
    border-radius: 50%;
    max-width: 100%;
    cursor: pointer;
  }
  &-right {
    color: #fff;
    text-align: center;
    letter-spacing: 5px;
    text-indent: 5px;
  }
  &-title {
    font-size: 2rem;
    font-weight: bold;
  }
  &-desc {
    margin-top: 30px;
    font-size: 1.2rem;
  }
}
.main {
  &-wrap {
    // background: #f4f4f4;
    padding: 30px 24px;
  }
}
.no-more {
  color: #555;
  text-align: center;
  font-size: 14px;
  padding-bottom: 30px;
}
</style>
