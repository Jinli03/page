<template>
  <div>
    <el-row>
      <el-col :span="8">
        <img src="../assets/logo1.jpg" alt="图标" style="width: 200px; height: 50px">
      </el-col>
      <el-col :span="8">
        <el-menu
            :default-active="activeIndex"
            class="el-menu-demo"
            mode="horizontal"
            @select="handleSelect"
        >
          <el-menu-item index="1" @click.native="$router.push('/')">首页</el-menu-item>
          <el-menu-item index="2" @click.native="$router.push('/123.pdf')">学者</el-menu-item>
          <el-menu-item index="3" @click.native="$router.push('/password')">成果</el-menu-item>
        </el-menu>
      </el-col>
      <el-col :span="8" style="margin-top: 10px">
        <el-row :gutter="20">
          <el-col :span="8">
            <el-button plain @click="handelregisterVisible()">登录|注册</el-button>
          </el-col>

          <el-col :span="8">
            <el-button plain @click.native="$router.push('/personal')">个人主页</el-button>
          </el-col>

          <el-col :span="8">
            <el-button plain>管理员主页</el-button>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
    <el-container class="background-image-container">
      <div style="margin: 10px; backdrop-filter: blur(2px); width: 600px; height: 80px; display: flex; justify-content:center">
        <div style="display: flex; justify-content: center; align-items: center;">
          <el-select
              v-model="value"
              placeholder="请选择"
              size="large"
              style="width: 130px"
          >
            <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
            />
          </el-select>
          <el-input
              v-model="input1"
              style="width: 240px; height: 40px"
              placeholder="请输入内容"
          />
          <el-button type="primary" style="height: 40px"><el-icon style="margin: 5px">
            <search />
          </el-icon></el-button>
        </div>
      </div>
    </el-container>
    <el-row :gutter="20" style="margin-top: 20px">
      <el-col :span="12">
        <el-statistic title="成果" :value="progress" />
      </el-col>
      <el-col :span="12">
        <el-statistic title="研究" :value="analyze" />
      </el-col>
    </el-row>
    <el-row>
      <el-container style="background-color: #d74764; width: 100%; height: 350px; margin-right: 30px; margin-left: 30px; margin-top: 20px">
        <el-header style="display: flex; justify-content: space-between;">
          <p style="margin-right: auto; margin-left: 10px; font-weight: bold; color: white">主要学者</p>
          <p style="margin-left: auto; margin-right: 10px; cursor: pointer; font-weight: bold; color: white" @click="">MORE</p>
        </el-header>
        <el-row :gutter="20" style="margin: 15px">
          <el-col :span="6">
            <el-card>
              <el-avatar
                  src="https://th.bing.com/th/id/OIP.eGxrXl3JBPvZ-9UeBRx0cgHaHa?rs=1&pid=ImgDetMain" style="width: 100px; height: 100px"
              />
              <p style="font-weight: bold">张三</p>
              <p></p>
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card>
              <el-avatar
                  src="https://th.bing.com/th/id/OIP.eGxrXl3JBPvZ-9UeBRx0cgHaHa?rs=1&pid=ImgDetMain" style="width: 100px; height: 100px"
              />
              <p style="font-weight: bold">张三</p>
              <p></p>
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card>
              <el-avatar
                  src="https://th.bing.com/th/id/OIP.eGxrXl3JBPvZ-9UeBRx0cgHaHa?rs=1&pid=ImgDetMain" style="width: 100px; height: 100px"
              />
              <p style="font-weight: bold">张三</p>
              <p></p>
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card>
              <el-avatar
                  src="https://th.bing.com/th/id/OIP.eGxrXl3JBPvZ-9UeBRx0cgHaHa?rs=1&pid=ImgDetMain" style="width: 100px; height: 100px"
              />
              <p style="font-weight: bold">张三</p>
              <p></p>
            </el-card>
          </el-col>
        </el-row>
      </el-container>
      <el-container style="background-color: #2a86be; width: 100%; height: 350px; margin-right: 30px; margin-left: 30px; margin-top: 15px">
        <el-header style="display: flex; justify-content: space-between;">
          <p style="margin-right: auto; margin-left: 10px; font-weight: bold; color: white">最新成果</p>
          <p style="margin-left: auto; margin-right: 10px; cursor: pointer; font-weight: bold; color: white" @click="">MORE</p>
        </el-header>
      </el-container>
    </el-row>
  </div>
  <el-dialog
      v-model="registerVisible"
      title="登录|注册"
      width="500"
      draggable
      overflow
  >
    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
      <el-tab-pane label="密码登录" name="first">
        <el-input v-model="account" style="width: 240px" placeholder="邮箱账号" />
        <el-input v-model="password" style="width: 240px; margin-top: 5px" placeholder="密码" />
      </el-tab-pane>
      <el-tab-pane label="验证码登录" name="second">
        <el-input v-model="phone" style="width: 240px" placeholder="手机号码" />
        <el-input v-model="code" style="width: 240px; margin-top: 5px" placeholder="验证码" />
      </el-tab-pane>
    </el-tabs>
    <el-row style="display: flex; justify-content: center; align-items: center;">
      <span style="color: dodgerblue; cursor: pointer;" @click="$router.push('/register')"> 忘记密码？</span>
    </el-row>
    <el-row style="display: flex; justify-content: center; align-items: center;">
      <el-button type="primary" @click="registerVisible = false">登录</el-button>
    </el-row>
    <template #footer>
      <div class="dialog-footer">
        <span style="color: dodgerblue; cursor: pointer" @click="$router.push('/register')"> 注册新账号</span>
      </div>
    </template>
  </el-dialog>
</template>

<script>
import { ref } from 'vue';
import { useTransition } from '@vueuse/core'

export default {
  name: 'HomeView',
  setup() {
    const activeIndex = ref('1')
    const registerVisible = ref(false)
    const input1 = ref('')
    const source = ref(0)
    const source1 = ref(0)
    const progress = useTransition(source, {
      duration: 1000,
    })
    source.value = 1200
    const analyze = useTransition(source1, {
      duration: 1000,
    })
    source1.value = 1200
    const value = ref('')
    const options = [
      {
        value: 'Option1',
        label: 'Option1',
      },
      {
        value: 'Option2',
        label: 'Option2',
      },
      {
        value: 'Option3',
        label: 'Option3',
      },
      {
        value: 'Option4',
        label: 'Option4',
      },
      {
        value: 'Option5',
        label: 'Option5',
      },
    ]
    const activeName = ref('first')
    const account =ref('')
    const password =ref('')
    const phone =ref('')
    const code =ref('')
    function handelregisterVisible() {
      registerVisible.value = true
    }
    return{
      activeIndex,
      input1,
      registerVisible,
      progress,
      analyze,
      handelregisterVisible,
      value,
      options,
      activeName,
      account,
      password,
      phone,
      code
    }
  },
}
</script>

<style lang="scss">
.background-image-container {
  background-image: url('@/assets/back.jpg');
  background-size: cover; /* 将背景图片铺满整个容器 */
  background-position: center; /* 图片居中显示 */
  height: 84vh; /* 调整容器的高度，根据需要更改 */
  background-size: 100%; /* 缩小背景图片 */
  display: flex;
  justify-content: center;
  align-items: center;
  color: white; /* 文字颜色 */
}
</style>
