<template>
<div class="layout">
  <Topnav class="nav" />
  <div class="content">
    <aside :class="menuVisible ? 'asideOpen': 'asideClosed'">
      <h2>文档</h2>
      <ol>
        <li>
          <router-link to="/doc/intro">介绍</router-link>
        </li>
        <li>
          <router-link to="/doc/install">安装</router-link>
        </li>
        <li>
          <router-link to="/doc/get-started">开始使用</router-link>
        </li>
      </ol>
      <h2>组件列表</h2>
      <ol>
        <li>
          <router-link to="/doc/switch">Switch 组件</router-link>
        </li>
        <li>
          <router-link to="/doc/button">Button 组件</router-link>
        </li>
        <li>
          <router-link to="/doc/dialog">Dialog 组件</router-link>
        </li>
        <li>
          <router-link to="/doc/tabs">Tabs 组件</router-link>
        </li>
      </ol>
    </aside>
    <main>
      <router-view />
    </main>
  </div>
</div>
</template>

<script lang="ts">
import Topnav from "../components/Topnav.vue";
import {
  inject,
  Ref
} from "vue";
export default {
  components: {
    Topnav
  },
  setup() {
    const menuVisible = inject < Ref < boolean >> ("menuVisible"); // get
    return {
      menuVisible
    };
  },
};
</script>

<style lang="scss" scoped>
$aside-index : 10;
$lightbgc: #e6f7ff;
$deepbgc: #1890ff;
$text: #262626;
.layout {
  display: flex;
  flex-direction: column;
  height: 100vh;

  >.nav {
    flex-shrink: 0;
  }

  >.content {
    flex-grow: 1;
    padding-top: 60px;
    padding-left: 156px;

    @media (max-width: 500px) {
      padding-left: 0;
    }
  }
}

.content {
  display: flex;

  >aside {
    flex-shrink: 0;
  }

  >main {
    flex-grow: 1;
    padding: 32px 64px;
    background: white;
  }
}
.asideOpen{
  height: 110vh;
  overflow: hidden;
}
.asideClosed{
  height: 0vh;
  overflow: hidden;
}
aside {
  width: 180px;
  position: fixed;
  box-shadow: 5px 0 5px rgba(#333, 0.1);
  background-color: white;
  top: 0;
  left: 0;
  padding-top: 70px;
  height: 100%;
  z-index: $aside-index;
  transition: all 0.4s cubic-bezier(0.68, 0.18, 0.53, 0.18) 0.1s;
  transition: height 0.5s;
  >h2 {
    margin-bottom: 4px;
    padding: 0 16px;
    margin-top: 16px;
  }
   > ol {
     line-height: 40px;
    > li {
      > a {
        position: relative;
        height: 40px;
        color: $text;
        display: block;
        padding: 2px 20px;
        text-decoration: none;
        &:hover {
          background: $lightbgc;
          border-bottom: none;
          color:#1890ff
        }
      }
      .router-link-active {
        background: $lightbgc;
        color: #1890ff;
        border-right: 3px solid $deepbgc;
        @media (min-width: 500px) {
          border-right: none;
        }
      }
    }
  }
}

main {
  overflow: auto;
}
</style>
