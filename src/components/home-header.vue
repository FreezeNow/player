<template>
  <header class="header">
    <div class="top">
      <button type="button" class="menuBtn" @click="menuClick">
        <span class="nm-icon"></span>
        <span class="nm-icon"></span>
        <span class="nm-icon"></span>
      </button>
    </div>
    <aside class="menu-box" :class="menuClass">
      <ul class="menu-list" v-if="isLogin">
        <li class="menu" v-for="(menu, index) of menuList" :key="index" @click="menuClick">
          <router-link :to="{ path: menu.href }">{{ menu.name }}</router-link>
        </li>
      </ul>
      <button type="button" class="exitBtn" v-if="isLogin" @click="exitClick">退出账号</button>
    </aside>
    <div class="menuBg" :class="menuClass" @click="menuClass.on = false"></div>
  </header>
</template>

<script>
// import toolbox from '@/assets/toolbox.js';

// const { cookie } = toolbox;
export default {
  name: 'vHeader',
  data() {
    return {
      menuClass: {
        on: false,
      },
      menuList: [
        { href: '/upload-file', name: '上传文件' },
        // { href: "/collection", name: "收藏" }
      ],
    };
  },
  computed: {
    isLogin() {
      return true;
    },
    user() {
      return {};
    },
  },
  methods: {
    menuClick() {
      console.log(this.menuClass);

      this.menuClass.on = !this.menuClass.on;
    },
    exitClick() {
      this.$store.commit('setIsLogin');
      this.$store.commit('setIsRefresh', {
        isRefresh: true,
      });
      this.$store.commit({
        type: 'setUser',
        id: -1,
        name: '',
        head: '',
        headportrait: '',
        motto: '',
        sex: '',
      });
      // cookie.deleteCookie('uid', {
      //   path: '/',
      // });
      this.menuClick();
    },
  },
  components: {},
};
</script>

<style lang="stylus" scoped>
.header {
  height: 100%;
  // position: relative;
}

.top {
  width: 100%;
  height: 40px;
  background-color: color-white;
  border-bottom 1px solid color-border
  position: relative;
  z-index: 20;
}

.menuBtn {
  margin: 5px;
  padding: 8px 5px 7px;
  float: left;
  background-color: rgba(0, 0, 0, 0);
  transition: background-color time-change;

  &:hover {
    background-color: rgba(0, 0, 0, 0.1);
  }
}

.nm-icon {
  margin-top: 3px;
  display: block;
  width: 20px;
  height: 3px;
  border-radius: 1px;
  background-color: color-theme;

  &:nth-child(1) {
    margin-top: 0;
  }
}

.menu-box {
  width: 250px;
  // height: 100%;
  background-color: #fff;
  position: fixed;
  top: 0;
  bottom: 0;
  left: -250px;
  z-index: 50;
  transition: left time-change;

  &.on {
    left: 0px;
  }
}

.menu-list {
  text-align: left;
}

.menu {
  & a {
    display: block;
    padding-left: 15px;
    height: height-base;
    color: color-black;
    line-height: height-base;
    border-bottom: 1px solid color-border;

    &:hover {
      background-color: (color-theme + 90%);
    }
  }
}

.exitBtn {
  display: block;
  width: 100%;
  height: height-base;
  position: absolute;
  bottom: 0;
  left: 0;
  background-color: color-theme;

  &:hover {
    background-color: color-white;
    color: color-theme;
  }
}

.menuBg {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 49;
  background-color: rgba(0, 0, 0, 0);
  transition: background-color time-change;
  visibility: hidden;

  &.on {
    visibility: visible;
    background-color: rgba(0, 0, 0, 0.5);
  }
}
</style>
