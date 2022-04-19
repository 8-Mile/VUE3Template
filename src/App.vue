<template>
<!-- <div @mousemove="isTimeOut"> -->
  <div>
   <el-config-provider :locale="locale" :size="size" >
    <router-view></router-view>
  </el-config-provider>
</div>
 
</template>

<script lang="ts">
import { number } from "echarts";
import { defineComponent, computed, reactive } from "vue";
import { useI18n } from "vue-i18n";
import { useStore } from "vuex";
import { ElMessage } from 'element-plus'
export default defineComponent({
  name: "App",
  setup() {
    const store = useStore();
    const i18n = useI18n();
    const size = computed(() => store.state.app.elementSize);
    const messages: any = i18n.messages.value;
    const locale = computed(() => {
      return {
        name: i18n.locale.value,
        el: messages[i18n.locale.value].el,
      };
    });
    const currentTime = new Date().getTime()
    const isTimeOut = () => {
      let currentTimes = currentTime;
      let lastTime = new Date().getTime();
      let timeOut = 1 * 60 * 1000; //设置时间 10分钟
      if (lastTime - currentTimes > timeOut) {
        // 未操作页面，跳转登录页面
        currentTimes = new Date().getTime();
        ElMessage.success({
          type: 'success',
          message: '长时间不操作跳转到登录页'
        })
        store.dispatch('user/loginOut')
      } else {
        currentTimes = new Date().getTime();
      }
    };
    return {
      locale,
      size,
      isTimeOut,
      currentTime
    };
    
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  height: 100vh;
}
</style>
