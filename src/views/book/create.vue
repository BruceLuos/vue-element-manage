<template>
  <el-breadcrumb separator="/">
    <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
    <el-breadcrumb-item>
      <a href="/">活动管理</a>
    </el-breadcrumb-item>
    <el-breadcrumb-item>活动列表</el-breadcrumb-item>
    <el-breadcrumb-item>活动详情</el-breadcrumb-item>
  </el-breadcrumb>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {

    }
  },
  created() {
    const url = '/book/home/v2'
    // 普通get请求,缺点每次请求都会添加token到header中
    // axios.get(url,{
    //   params: { openId: '1234' },
    //   header: { token: 'abcd'}
    // }).then(response => {
    //   console.log(response)
    // }).catch(err => {
    //   console.log(err)
    // })

    // 自定义axios实例
    // const request = axios.create({
    //   baseURL: 'https://test.youbaobao.xyz:18081',
    //   timeout: 5000
    // })
    // request({
    //   url,
    //   method: 'get',
    //   params: {
    //     openId: '1234'
    //   }
    // }).then(response => {
    //   console.log(response.data)
    // })

    const whiteUrl = ['/login']
    const request = axios.create({
      baseURL: 'https://test.youbaobao.xyz:18081',
      timeout: 5000
    })
    // axios请求拦截器
    request.interceptors.request.use(config => {
      console.log(config)
      const url = config.url.replace(config.baseURL, '')
      if (whiteUrl.some(w1 => url === w1)) {
        return config
      }
      config.headers['token'] = 'abcd'
      return config
    }, error => {
      return Promise.reject(error)
    })

    // axios响应拦截器
    request.interceptors.response.use(response => {
      console.log(response)
      const res = response.data
      if (res.error_code !== 0) {
        alert(res.msg)
        return Promise.reject(new Error(res.msg))
      } else {
        return res
      }
    }, error => {
      return Promise.reject(error)
    })
    request({
      url,
      method: 'get',
      params: {
        openId: '1234'
      }
    }).then(response => {
      console.log(response.data)
    }).catch(err => {
      console.log(err)
    })
  }
}
</script>
<style lang='scss' scoped>
//@import url(); 引入公共css类
</style>
