<template>
  <v-row justify="center">
    <v-dialog v-model="isActive" max-width="600px" @click="cancel">
      <v-card>
        <v-card-title>
          <span class="headline">Settings</span>
        </v-card-title>
        <v-card-text>
          <v-text-field type="number" v-model="newSettings.width" label="Field Width" />
          <v-text-field type="number" v-model="newSettings.height" label="Field Height" />
          <v-select
            v-model="newSettings.scale"
            :items="scales"
            item-value="value"
            item-text="name"
          />
          <v-checkbox v-model="newSettings.isFluid" label="Fluid" />
          <v-checkbox v-model="newSettings.showGrid" label="Show Grid" />
        </v-card-text>
        <v-card-actions>
          <v-btn @click="ok" color="primary">OK</v-btn>
          <v-btn @click="cancel">Cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  props: {
    isActive: {
      type: Boolean,
      default: false
    },
    settings: {
      type: Object,
      default() {
        return {
          width: 1500,
          height: 1000,
          scale: "1",
          isFluid: false,
          showGrid: false
        };
      }
    }
  },
  watch: {
    isActive(val) {
      if (val) {
        this.newSettings = Object.assign({}, this.settings);
      }
    }
  },
  data() {
    return {
      newSettings: {
        width: 0,
        height: 0,
        showGrid: false
      },
      scales: [
        { value: "0.5", name: "Small"},
        { value: "1", name: "Medium" },
        { value:"2", name: "Large" }
      ]
    };
  },
  methods: {
    changeGrid() {
      this.$emit("changeGrid");
    },
    ok() {
      this.$emit("ok", this.newSettings);
    },
    cancel() {
      this.$emit("cancel");
    }
  }
};
</script>
