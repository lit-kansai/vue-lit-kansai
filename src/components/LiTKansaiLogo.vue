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
  <div id="splash-logo"></div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Lottie from "lottie-web";
import { logo, notfound } from "@/anim";

@Component
export default class LiTKansaiLogo extends Vue {
  @Prop({ default: true })
  autoplay?: boolean;

  @Prop({ default: false })
  notfound?: boolean;

  mounted() {
    const logoContainer = document.getElementById("splash-logo");
    if (!logoContainer) return;
    setTimeout(() => {
      const anim = Lottie.loadAnimation({
        container: logoContainer,
        animationData: this.notfound ? notfound : logo,
        renderer: "svg",
        loop: false,
        autoplay: this.autoplay
      });
      anim.addEventListener("complete", () => this.$emit("completed"));
    }, 200);
  }
}
</script>
