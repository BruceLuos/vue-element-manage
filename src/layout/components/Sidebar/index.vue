<template>
  <div :class="{'has-logo':showLogo}">
    <logo v-if="showLogo" :collapse="isCollapse" />
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-menu
        :default-active="activeMenu"
        :collapse="isCollapse"
        :background-color="variables.menuBg"
        :text-color="variables.menuText"
        :unique-opened="false"
        :active-text-color="variables.menuActiveText"
        :collapse-transition="false"
        mode="vertical"
      >
      <!-- 向这个组件传入permisson routes的路由进行遍历 -->
        <sidebar-item v-for="route in permission_routes" :key="route.path" :item="route" :base-path="route.path" />
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Logo from './Logo'
import SidebarItem from './SidebarItem'
import variables from '@/styles/variables.scss'

export default {
  components: { SidebarItem, Logo },
  computed: {
    ...mapGetters([
      'permission_routes',
      'sidebar'
    ]),
    activeMenu() {
      const route = this.$route
      const { meta, path } = route
      // if set path, the sidebar will highlight the path you set
      if (meta.activeMenu) {
        return meta.activeMenu
      }
      return path
    },
    showLogo() {
      return this.$store.state.settings.sidebarLogo
    },
    variables() {
      return variables
    },
    isCollapse() {
      return !this.sidebar.opened
    }
  }
}
</script>
/*sidebar：sidebar 主要包含 el-menu 容器组件，el-menu 中遍历 vuex 中的 routes，生成 sidebar-item 组件。sidebar 主要配置项如下：
activeMenu：根据当前路由的 meta.activeMenu 属性控制侧边栏中高亮菜单
isCollapse：根据 Cookie 的 sidebarStatus 控制侧边栏是否折叠
variables：通过 @/styles/variables.scss 填充 el-menu 的基本样式
sidebar-item：sidebar-item 分为两部分：
第一部分是当只需要展示一个 children 或者没有 children 时进行展示，展示的组件包括：
app-link：动态组件，path 为链接时，显示为 a 标签，path 为路由时，显示为 router-link 组件
el-menu-item：菜单项，当 sidebar-item 为非 nest 组件时，el-menu-item 会增加 submenu-title-noDropdown 的 class
item：el-menu-item 里的内容，主要是 icon 和 title，当 title 为空时，整个菜单项将不会展示
第二部分是当 children 超过两项时进行展示，展示的组件包括：
el-submenu：子菜单组件容器，用于嵌套子菜单组件
sidebar-item：el-submenu 迭代嵌套了 sidebar-item 组件，在 sidebar-item 组件中有两点变化：
设置 is-nest 属性为 true
根据 child.path 生成了 base-path 属性传入 sidebar-item 组件 */
