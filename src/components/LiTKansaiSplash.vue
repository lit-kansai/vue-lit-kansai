<!--
  Copyright 2020 LiT Kansai
 
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at
  
      http://www.apache.org/licenses/LICENSE-2.0
  
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->

<template>
  <transition name="fade">
    <div id="splash" v-if="isSplashing">
      <LiTKansaiLogo @completed="onCompleted" :notfound="notfound" />
    </div>
  </transition>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import LiTKansaiLogo from "@/components/LiTKansaiLogo.vue";

@Component({ components: { LiTKansaiLogo } })
export default class LiTKansaiSplash extends Vue {
  isSplashing = true;

  @Prop({ default: false })
  notfound?: boolean;

  onCompleted() {
    setTimeout(() => {
      if (!this.notfound) this.isSplashing = false;
    }, 200);
  }
}
</script>

<style scoped>
#splash {
  background: #fcfcfc;
  position: fixed;
  width: 100vw;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 500;
  display: flex;
  justify-content: center;
  align-items: center;
}
#splash-logo {
  max-width: 400px;
  width: 75%;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
