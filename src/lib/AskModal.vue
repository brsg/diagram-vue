<template>
  <v-row justify="center">
    <v-dialog v-model="isActive" max-width="400px" persistent @click="cancel">
      <v-card>
        <v-card-text>
          <slot></slot>
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
  },
  methods: {
    ok() {
      this.$emit("ok", true);
    },
    cancel() {
      this.$emit("cancel");
    }
  }
};
</script>
<style lang="scss" scoped>
.inner-block {
  margin-bottom: 20px;
}
.block {
  padding: 40px;
}
input {
  margin-bottom: 5px;
}
.item-enter-active {
  transition: all 0.8s ease;
}
.item-leave-active {
  transition: all 0.3s ease;
}
.item-enter,
.item-leave-to {
  opacity: 0;
}
</style>
