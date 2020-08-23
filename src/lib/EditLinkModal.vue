<template>
  <v-row justify="center">
    <v-dialog v-model="isActive" max-width="600px" @click="cancel">
      <v-card>
        <v-card-title>
          <span class="headline">Edit Link</span>
        </v-card-title>
        <v-card-text>
          <v-text-field type="text" v-model="newLink.color" label="Color" outlined dense />
          <v-select
            v-model="newLink.shape"
            :items="shapes"
            item-text="name"
            item-value="value"
            label="Shape"
            outlined
            dense
          />
          <v-select
            v-model="newLink.pattern"
            :items="patterns"
            item-text="name"
            item-value="value"
            label="Line Pattern"
            outlined
            dense
          />
          <v-select
            v-model="newLink.arrow"
            :items="arrows"
            item-text="name"
            item-value="value"
            label="Arrow Type"
            outlined
            dense
          />
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
    link: {
      type: Object,
      default() {
        return {
          id: "0",
          content: {
            color: "#ffeaa7",
            shape: "straight",
            pattern: "solid",
            arrow: "none"
          }
        };
      }
    }
  },
  data() {
    return {
      shapes: [
        { value: "straight", name: "Straight Line" },
        { value: "bezier", name: "Bezier Curve" },
      ],
      patterns: [
        { value: "solid", name: "Solid" },
        { value: "dash", name: "Dash" },
        { value: "dot", name: "Dot" },
      ],
      arrows: [
        { value: "none", name: "None" },
        { value: "src", name: "One Side (Dource)" },
        { value: "dest", name: "One Side (Destination)" },
        { value: "both", name: "Both Sides" },
      ],
    };
  },
  computed: {
    newLink: {
      get() {
        return this.link.content;
      }
    }
  },
  methods: {
    ok() {
      this.$emit("ok", {
        id: this.link.id,
        content: {
          color: this.newLink.color,
          shape: this.newLink.shape,
          pattern: this.newLink.pattern,
          arrow: this.newLink.arrow
        }
      });
    },
    cancel() {
      this.$emit("cancel");
    }
  }
};
</script>
<style lang="scss" scoped>
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
select {
  margin-bottom: 5px;
}
</style>
