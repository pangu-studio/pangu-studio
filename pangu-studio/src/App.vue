<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref, onMounted } from "vue";
import { useDark, useToggle } from "@vueuse/core";
import { invoke } from "@tauri-apps/api/tauri";
import {
  Document,
  Menu as IconMenu,
  Expand,
  Fold,
  Setting,
} from "@element-plus/icons-vue";

let activeClass = "el-menu--collapse";

const isCollapse = ref(true);
let isDark = useDark();
const handleOpen = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};
const toggleDark = useToggle(isDark);
onMounted(() => {
  // invoke("init",{env: import.meta.env.MODE}).then((_) => {
  //   // return null
  // }).catch((err) => {
  //   console.log(err)
  // }).finally(() => {
  //   console.log("init finished")
  // });
});

// function toggleDark() {
//   useToggle(isDark)
// }
</script>

<template>
  <el-container class="container">
    <el-aside width="120px" class="aside" :class="isCollapse ? activeClass : ''">
      <el-menu default-active="2" class="el-menu-vertical-demo" :collapse="isCollapse" @open="handleOpen" router
        :collapse-transition="false" @close="handleClose">
        <el-menu-item class="logo">
          <img src="@/assets/logo.png" style="width: 32px" />
          <template #title>
            <div>Pangu Studio</div>
          </template>
        </el-menu-item>

        <el-menu-item index="/">

          <!-- <UploadFilled /> -->
          <icon-cib-docker class="menu-icon" />
          <template #title>容器</template>
        </el-menu-item>
        <el-menu-item index="/appstore">
          <icon-ion-md-appstore class="menu-icon" />
          <template #title>商店</template>
        </el-menu-item>
        <el-menu-item index="/filemanager">
          <icon-ion-file-tray-full-sharp class="menu-icon" />
          <template #title>文件</template>
        </el-menu-item>
        <el-menu-item index="/sslcert/certificates">
          <icon-mdi-certificate class="menu-icon" />
          <template #title>证书</template>
        </el-menu-item>
        <el-menu-item index="/setting">
          <icon-ion-settings class="menu-icon" />
          <template #title>设置</template>
        </el-menu-item>
      </el-menu>
      <div class="bottom-tool" :class="isCollapse ? activeClass : 'bt-ex'">
        <el-switch class="dark-switch" inline-prompt active-text="黑" inactive-text="白" v-model="isDark"
          :change="useToggle()" size="small" />

        <el-button circle class="ex-btn" v-if="isCollapse" @click="isCollapse = !isCollapse" :icon="Expand" />
        <el-button circle class="ex-btn" v-if="!isCollapse" @click="isCollapse = !isCollapse" :icon="Fold" />
      </div>
    </el-aside>
    <el-main class="main">
      <router-view />
    </el-main>
  </el-container>
</template>

<style lang="scss" scoped>
.main {
  margin: 0;
  padding: 0;
  height: 100%;
}

.logo {
  justify-content: center;
  flex-direction: column;
  display: flex;
  // align-items: center;
  // height: 90px;

  img {
    cursor: pointer;
    margin-left: -5px;
  }

  div {
    font-weight: 500;
    width: 100%;
  }
}

.logo:hover {
  background: none;
}

.logo.vite:hover {
  filter: drop-shadow(0 0 2em #747bff);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #249b73);
}

h1 {
  text-align: center;
}

.btn {
  width: 100px;
  margin: 0 auto;
}

.el-menu-vertical-demo {
  min-height: 100%;
}


.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 120px;
  min-height: 100%;

  .menu-icon {
    padding-right: 8px;
  }

  .logo {
    flex-wrap: wrap;
    height: 80px;

    img {
      margin-top: -20px;

    }

    div {
      // color: #333;
      height: 8px;
      margin-top: -10px;
      margin-left: -5px;
    }


  }
}

.aside {

  // height: 100%;
  .bt-ex {
    width: 120px;
  }

  .bottom-tool {
    position: fixed;
    bottom: 10px;
    overflow: hidden;
    z-index: 9999;
    position: fixed;
    text-align: center;
    margin: 0 auto;

    .dark-switch {
      margin: 0 auto;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .ex-btn {
      margin: 0 auto;
      border: none;
    }
  }
}

.container {
  height: 100%;
}

.menu-icon {
  // padding-right: 8px;

}

</style>
