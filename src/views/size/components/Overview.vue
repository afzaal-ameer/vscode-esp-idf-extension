<template>
  <div class="notification is-clipped">
    <nav class="level is-mobile">
      <div class="level-item has-text-centered">
        <div>
          <p class="heading is-size-7-mobile">.data</p>
          <p class="title is-size-5-mobile">
            {{ convertToKB(this.getArchiveProp("diram_data", "dram_data")) }}KB
          </p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading is-size-7-mobile">.bss</p>
          <p class="title is-size-5-mobile">
            {{ convertToKB(this.getArchiveProp("diram_bss", "dram_bss")) }}KB
          </p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading is-size-7-mobile">Text</p>
          <p class="title is-size-5-mobile">
            {{ convertToKB(this.getArchiveProp("diram_text", "dram_text")) }}KB
          </p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading is-size-7-mobile">Flash Code</p>
          <p class="title is-size-5-mobile">
            {{ convertToKB(overviewData.flash_code) }}KB
          </p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading is-size-7-mobile">Flash Rodata</p>
          <p class="title is-size-5-mobile">
            {{ convertToKB(overviewData.flash_rodata) }}KB
          </p>
        </div>
      </div>
      <div class="level-item has-text-centered" v-if="overviewData.flash_other">
        <div>
          <p class="heading is-size-7-mobile">Flash other</p>
          <p class="title is-size-5-mobile">
            {{ convertToKB(overviewData.flash_other) }}KB
          </p>
        </div>
      </div>
    </nav>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { State } from "vuex-class";

@Component
export default class Overview extends Vue {
  @State("overviewData") storeOverviewData;

  convertToKB(byte: number) {
    return typeof byte === "number" ? Math.round(byte / 1024) : 0;
  }

  get overviewData() {
    return this.storeOverviewData;
  }

  getArchiveProp(prop1: string, prop2: string) {
    return Object.keys(this.storeOverviewData).indexOf(prop1) !== -1
      ? this.storeOverviewData[prop1]
      : this.storeOverviewData[prop2];
  }
}
</script>
