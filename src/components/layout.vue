<template>
<a-layout class="layout" id="components-layout-demo-side" style="min-height: 100vh">
  <a-layout-sider class="left-nav" v-if="showNav">
    <LaftNav />
  </a-layout-sider>
  <a-layout class="content">
    <a-layout-content>
        <transition>
          <keep-alive>
            <router-view></router-view>
          </keep-alive>
        </transition>
    </a-layout-content>
    <!-- <a-layout-footer style="text-align: center">
        Ant Design ©2018 Created by Ant UED
      </a-layout-footer> -->
  </a-layout>
</a-layout>
</template>

<script>
import LaftNav from './laft-nav.vue'
export default {
  data() {
    return {
      collapsed: false,
      showNav: false // false --> closed leftNav
    };
  },
  components: {
    LaftNav
  }
};
</script>

<style lang="less">
.layout {
  
  .left-nav {
    // position: fixed;
    // height: 100%;
    // overflow: auto;
    .ant-layout-sider-trigger{
      // display: none;
    }
  }
  .content{
    background: #f1f0ef;
  }
}
</style>
