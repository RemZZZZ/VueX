# VueX

安装vuex
        
    npm install vuex --save
         
新建store文件夹，并创建index.js，全局注入

    import store from './store'//引入store
 
    new Vue({
      el: '#app',
      store,//使用store
      template: '<App/>',
      components: { App }
    })
    
index.js

声明state变量

    import Vue from 'vue'
    import Vuex from 'vuex'
    Vue.use(Vuex)
    
    const state = {
      user: '',
      psd: ''
    }
    
vuex官方API提供了一个getters，和vue计算属性computed一样，来实时监听state值的变化(最新状态)

    import Vue from 'vue'
    import Vuex from 'vuex'
    Vue.use(Vuex)
    const state = {
      user: '',
      psd: ''
    }
    const getters = {
      getUser () {
        return state.user
      }
    }
    
mutations用于改变state的值

    import Vue from 'vue'
    import Vuex from 'vuex'
    Vue.use(Vuex)
    const state = {
      user: '',
      psd: ''
    }
    const getters = {
      getUser () {
        return state.user
      }
    }
    const mutations = {
      setUser (state, value) {
        state.user = value
      }
    }
    
这时候你完全可以用 this.$store.commit('setUser',value) 在别的组件里面进行改变user的值了，但这不是理想的改变值的方式；因为在 Vuex 中，mutations里面的方法 都是同步事务，意思就是说：比如这里的一个this.$store.commit('setUser',value)方法,两个组件里用执行得到的值，每次都是一样的，这样肯定不是理想的需求

vuex官方API还提供了一个actions，这个actions也是个对象变量，最大的作用就是里面的Action方法 可以包含任意异步操作，这里面的方法是用来异步触发mutations里面的方法，actions里面自定义的函数接收一个context参数和要变化的形参，context与store实例具有相同的方法和属性，所以它可以执行context.commit(' ')

    import Vue from 'vue'
    import Vuex from 'vuex'
    Vue.use(Vuex)
    const state = {
      user: '',
      psd: ''
    }
    const getters = {
       getUser () {
         return state.user
       }
    }
    const mutations = {
      setUser (state, value) {
        state.user = value
      }
    }
    const actions = {
      setUser (context, value) {
        context.commit('setUser', value)
      }
    }
    const store = new Vuex.Store({
      state,
      getters,
      mutations,
      actions
    })
    export default store
    
全局给user赋值

    this.$store.dispatch('setUser', value)
    
全局获取

    this.$store.getters.getUser
