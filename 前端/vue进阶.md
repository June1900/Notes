#  一、vue-cli脚手架



#  二、vue-router



#  三、vuex

##  vuex

* vuex是什么
  * 专门为vue开发的状态管理模式。采用集中式存储管理应用的所有状态，以相应的规则保证状态一种可预测的方式发生变化
  * 状态
* 使用Vuex
  * 安装vuex模块
    * npm install vuex --save
  * 作为插件使用
    * Vue.use(Vuex)
  * 定义容器
    * new Vuex.Store()
  * 注入根实例
    * { store }
* 使用mock数据
  * easy-mock
* 什么情况下使用vuex
  * 多个视图依赖同一状态
  * 来自不同的视图的行为需要变更同一状态

# 四、axios

* 简介
  * 基于promise用于浏览器和Nodejs的与服务端通信的通信库
* 特性
  * 支持promise api
  * 拦截请求和响应
  * 转换请求和响应数据
  * 取消请求
  * 自动转换json数据
* 使用
  * cdn地址：
* 使用axios
  * 需要在使用的模块中引入
    * import axios from ‘axios’
  * 