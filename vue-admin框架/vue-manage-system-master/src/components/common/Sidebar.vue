<template>
    <div class="sidebar">
        <div class="seek-box">
            <el-input class="seek" v-model="input" placeholder="请输入内容" suffix-icon="el-icon-search"></el-input>
        </div>
        <el-menu class="sidebar-el-menu" :default-active="onRoutes" :collapse="collapse" background-color="#1A3459"
            text-color="#bfcbd9" active-text-color="#20a0ff" unique-opened router>
            <template v-for="item in items">
                <template v-if="item.subs">
                    <el-submenu :index="item.index" :key="item.index">
                        <template slot="title">
                            <i :class="item.icon"></i><span slot="title">{{ item.title }}</span>
                        </template>
                        <template v-for="subItem in item.subs">
                            <el-submenu v-if="subItem.subs" :index="subItem.index" :key="subItem.index">
                                <template slot="title">{{ subItem.title }}</template>
                                <el-menu-item v-for="(threeItem,i) in subItem.subs" :key="i" :index="threeItem.index">
                                    {{ threeItem.title }}
                                </el-menu-item>
                            </el-submenu>
                            <el-menu-item v-else :index="subItem.index" :key="subItem.index">
                                {{ subItem.title }}
                            </el-menu-item>
                        </template>
                    </el-submenu>
                </template>
                <template v-else>
                    <el-menu-item :index="item.index" :key="item.index">
                        <i :class="item.icon"></i><span slot="title">{{ item.title }}</span>
                    </el-menu-item>
                </template>
            </template>
        </el-menu>
    </div>
</template>

<script>
import bus from "../common/bus";
export default {
  data() {
    return {
      input: "",
      collapse: false,
      items: [
        {
          icon: "el-icon-lx-home",
          index: "dashboard",
          title: "系统首页"
        },
        {
          icon: "el-icon-lx-cascades",
          index: "table",
          title: "基础表格"
        },
        {
          icon: "el-icon-lx-copy",
          index: "tabs",
          title: "tab选项卡"
        },
        {
          icon: "el-icon-lx-calendar",
          index: "3",
          title: "表单相关",
          subs: [
            {
              index: "form",
              title: "基本表单"
            },
            {
              index: "3-2",
              title: "三级菜单",
              subs: [
                {
                  index: "editor",
                  title: "富文本编辑器"
                },
                {
                  index: "markdown",
                  title: "markdown编辑器"
                }
              ]
            },
            {
              index: "upload",
              title: "文件上传"
            }
          ]
        },
        {
          icon: "el-icon-lx-emoji",
          index: "icon",
          title: "自定义图标"
        },
        {
          icon: "el-icon-lx-favor",
          index: "charts",
          title: "schart图表"
        },
        {
          icon: "el-icon-rank",
          index: "drag",
          title: "拖拽列表"
        },
        {
          icon: "el-icon-lx-warn",
          index: "6",
          title: "错误处理",
          subs: [
            {
              index: "permission",
              title: "权限测试"
            },
            {
              index: "404",
              title: "404页面"
            }
          ]
        }
      ]
    };
  },
  computed: {
    onRoutes() {
      return this.$route.path.replace("/", "");
    }
  },
  created() {
    // 通过 Event Bus 进行组件间通信，来折叠侧边栏
    bus.$on("collapse", msg => {
      this.collapse = msg;
    });
  }
};
</script>
<style>
.seek-box input {
  width: 100%;
  height: 30px;
  background: rgba(45, 83, 123, 1);
  border-radius: 3px;
  border: 0;
  color: #fff;
}
</style>

<style lang="scss" scoped>
.sidebar {
  display: block;
  width: 230px;
  position: absolute;
  left: 0;
  top: 80px;
  bottom: 0;
  overflow-y: scroll;
  background-color: #1a3459;
  .seek-box {
    width: 100%;
    margin-top: 14px;
    box-sizing: border-box;
    padding: 0 22px;
  }
}
.sidebar::-webkit-scrollbar {
  width: 0;
}
.sidebar-el-menu:not(.el-menu--collapse) {
  width: 230px;
}
.sidebar > ul {
  height: 100%;
}
</style>
