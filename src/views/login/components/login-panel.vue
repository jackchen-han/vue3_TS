<template>
  <div class="login-panel">
    <h1 class="title">后台管理系统</h1>
    <el-tabs type="border-card" stretch v-model="currentTab">
      <el-tab-pane name="account">
        <template #label>
          <span class="icon-text">
            <el-icon><UserFilled /></el-icon>
            账号登陆
          </span>
        </template>
        <login-account ref="accountRef" />
      </el-tab-pane>
      <el-tab-pane name="phone">
        <template #label>
          <el-icon><Iphone /></el-icon>
          手机登陆
        </template>
        <login-phone />
      </el-tab-pane>
    </el-tabs>

    <div class="account-control">
      <el-checkbox v-model="isKeepPassword">记住密码</el-checkbox>
      <el-link type="primary">忘记密码</el-link>
    </div>

    <el-button type="primary" class="login-btn" @click="handleLoginClick"
      >立即登陆</el-button
    >
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import LoginAccount from './login-account.vue'
import LoginPhone from './login-phone.vue'

export default defineComponent({
  components: {
    LoginAccount,
    LoginPhone
  },
  setup() {
    // 1.定义属性
    const isKeepPassword = ref(false)
    // typeof 可以检测当前对象的类型
    const accountRef = ref<InstanceType<typeof LoginAccount>>()
    const currentTab = ref<string>('account')
    // 2.定义方法
    const handleLoginClick = (): void => {
      if (currentTab.value === 'account') {
        // 类型限制的情况下要加上可选链的语法
        accountRef.value?.loginAction(isKeepPassword.value)
      } else {
        console.log('调用手机号登陆的方法')
      }
    }
    return {
      isKeepPassword,
      accountRef,
      currentTab,
      handleLoginClick
    }
  }
})
</script>

<style scoped lang="less">
.login-panel {
  width: 320px;
  margin-bottom: 150px;
  .icon-text {
    vertical-align: middle;
    el-icon {
      line-height: 20px;
    }
  }
  .title {
    text-align: center;
  }
  .account-control {
    margin-top: 8px;
    display: flex;
    justify-content: space-between;
  }

  .login-btn {
    width: 100%;
    margin-top: 10px;
  }
}
</style>
