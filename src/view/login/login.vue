<style lang="less">
  @import './login.less';
</style>

<template>
  <div class="login">
    <div class="login-con">
      <Card icon="log-in" title="欢迎登录" :bordered="false">
        <div class="form-con">
          <login-form @on-success-valid="handleSubmit"></login-form>
          <p class="login-tip">输入任意用户名和密码即可</p>
        </div>
      </Card>
    </div>
  </div>
</template>

<script>
import LoginForm from '_c/login-form'
import { mapActions } from 'vuex'
import Main from '@/view/main'
import page404 from '@/view/error-page/404.vue'
export default {
  components: {
    LoginForm
  },
  methods: {
    ...mapActions([
      'handleLogin',
      'getUserInfo'
    ]),
    handleSubmit ({ userName, password }) {
      this.handleLogin({ userName, password }).then(res => {
        this.getUserInfo().then(res => {

          const routers = [{
            path: '/a',
            name: 'a',
            component: Main,
            meta: {
              title: 'AAA'
            },
            children: [
              {
                path: 'b',
                name: 'b',
                meta: {
                  icon: 'md-flower',
                  title: 'BBB'
                },
                component: page404
              }
            ]
          }]

          this.$router.addRoutes(routers);//调用

          console.log('router->',this.$router)

          this.$router.push({
            name: 'home'
          })
        })
      })
    }
  }
}
</script>

<style>

</style>
