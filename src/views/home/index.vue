<template>
<!-- 最外层放大容器 小容器放到大容器里 -->
  <el-container>
    <el-aside>
      <h1>左侧导航区域</h1>
    </el-aside>
    <!-- 右侧 嵌套 一个 el-container -->
    <el-container>
      <!-- 上下布局 -->
      <el-header>
        <h1>顶部操作栏</h1>
      </el-header>
      <!-- 主要区域 -->
      <el-main>
        <h1>主要区域</h1>
        <!-- 二级路由容器 -->
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
}
</script>

<style>
</style>
