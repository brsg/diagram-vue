<template>
  <v-row justify="center">
    <v-dialog v-model="isActive" max-width="400px" @click="cancel">
      <v-card>
        <v-card-title>
          <span class="headline">Import / Export</span>
        </v-card-title>
        <v-card-text>
          <v-textarea v-model="tmp" required outlined placeholder="JSON"></v-textarea>
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
    isActive: Boolean,
    text: String
  },
  watch: {
    text(val) {
      this.tmp = val;
    }
  },
  data() {
    return {
      tmp: ""
    };
  },
  methods: {
    ok() {
      this.$emit("ok", {
        text: this.tmp
      });
    },
    cancel() {
      this.$emit("cancel");
    }
  }
};
</script>
<style lang="scss" scoped>
.input {
  width: 100%;
  height: 100px;
  margin-bottom: 5px;
}
</style>
