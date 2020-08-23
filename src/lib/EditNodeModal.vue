<template>
  <v-row justify="center">
    <v-dialog v-model="isActive" max-width="600px" @click="cancel">
      <v-card>
        <v-card-title>
          <span class="headline">Edit Node</span>
        </v-card-title>
        <v-card-text>
          <v-text-field type="text" v-model="newNode.content.text" label="Name" outlined dense />
          <v-text-field type="text" v-model="newNode.content.url" label="Url" outlined dense />
          <v-text-field type="text" v-model="newNode.content.color" label="Color" outlined dense />
          <v-text-field type="number" v-model="newNode.width" label="Width" outlined dense />
          <v-text-field type="number" v-model="newNode.height" label="Height" outlined dense />
          <v-text-field type="text" v-model="newNode.stroke" label="Stroke" outlined dense />
          <v-text-field type="number" v-model="newNode.strokeWeight" label="Stroke Weight" outlined dense />
          <v-select
            v-model="newNode.shape"
            :items="shapes"
            item-text="name"
            item-value="value"
            label="Select Shape"
            outlined
            dense />
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
    node: {
      type: Object,
      default() {
        return {
          id: "",
          shape: "rectangle",
          width: 150,
          height: 60,
          stroke: "",
          strokeWeight: 0,
          content: {
            text: "none",
            url: "",
            color: "#ecf0f1"
          }
        };
      }
    }
  },
  watch: {
    node() {
      this.newWidth = parseInt(this.node.width);
      this.newHeight = parseInt(this.node.Height);
    }
  },
  data() {
    return {
      newNode: this.node,
      shapes: [
        { value: "rectangle", name: "Rectangle" },
        { value: "ellipse", name: "Elipse" },
      ],
    };
  },
  methods: {
    ok() {
      this.$emit("ok", this.newNode);
    },
    cancel() {
      this.$emit("cancel");
    }
  }
};
</script>
<style lang="scss" scoped>
input {
  width: 95%;
  margin-bottom: 5px;
}
select {
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
