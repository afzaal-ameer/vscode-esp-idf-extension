<template>
  <tr :class="{ error: error }">
    <td>
      <input
        class="input is-size-7-mobile is-size-7-tablet"
        type="text"
        placeholder="Name"
        maxlength="16"
        v-model="sName"
      />
    </td>
    <td class="w-md">
      <v-select
        :options="types"
        v-model="sType"
        placeholder="Type"
        taggable
        selectOnTab
      />
    </td>
    <td class="w-md">
      <v-select
        :options="subtypes"
        v-model="sSubType"
        label="label"
        placeholder="Sub Type"
        taggable
        selectOnTab
      />
    </td>
    <td>
      <input
        class="input is-size-7-mobile is-size-7-tablet"
        type="text"
        placeholder="Offset"
        v-model="sOffset"
      />
    </td>
    <td>
      <input
        class="input is-size-7-mobile is-size-7-tablet"
        type="text"
        placeholder="Size"
        v-model="sSize"
      />
    </td>
    <td><input type="checkbox" v-model="sFlag" /></td>
    <td>
      <a class="delete" @click="del"></a>
      <span
        class="icon is-small has-tooltip-arrow"
        :data-tooltip="error"
        v-if="error"
      >
        <iconify-icon icon="question" />
      </span>
    </td>
  </tr>
</template>

<script lang="ts">
import "vue-select/dist/vue-select.css";
import { Component, Emit, Prop, PropSync, Vue } from "vue-property-decorator";
import { PartitionTable } from "../store";
import vSelect from "vue-select";
Vue.component("v-select", vSelect);

@Component
export default class Row extends Vue {
  @PropSync("name") sName: String;
  @PropSync("type") sType: String;
  @PropSync("subtype") sSubType: String;
  @PropSync("offset") sOffset: String;
  @PropSync("size") sSize: String;
  @PropSync("flag") sFlag: String;
  @Prop() error: string;

  public get subtypes(): String[] {
    if (this.sType === "app") {
      return [
        "factory",
        "ota_0",
        "ota_1",
        "ota_2",
        "ota_3",
        "ota_4",
        "ota_5",
        "ota_6",
        "ota_7",
        "ota_8",
        "ota_9",
        "ota_10",
        "ota_11",
        "ota_12",
        "ota_13",
        "ota_14",
        "ota_15",
        "test",
      ];
    } else if (this.sType === "data") {
      return ["fat", "ota", "phy", "nvs", "nvs_keys", "spiffs","coredump"];
    }
    return [];
  }

  get types(): String[] {
    return ["app", "data"];
  }

  @Emit("delete")
  del() {}
}
</script>

<style>
.vs__dropdown-toggle {
  background-color: var(--vscode-input-background);
  border-color: var(--vscode-input-background);
  color: var(--vscode-input-foreground);
}
.vs__open-indicator,
.vs__clear {
  fill: var(--vscode-button-background);
}
.vs--single .vs__selected {
  color: var(--vscode-foreground);
}
.vs__search {
  color: var(--vscode-foreground);
}
.vs__search::placeholder {
  color: var(--vscode-input-placeholderForeground);
}
.vs__dropdown-menu {
  background-color: var(--vscode-input-background);
  border-color: var(--vscode-input-background);
}
.vs__dropdown-option {
  color: var(--vscode-foreground);
}
.vs__dropdown-option--highlight {
  background-color: var(--vscode-button-background);
  color: var(--vscode-foreground);
}
.w-md {
  min-width: 130px;
}
.error {
  background-color: rgba(176, 81, 41, 0.1);
}
</style>
