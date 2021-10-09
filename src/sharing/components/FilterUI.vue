<template>
  <div class="filter">
    <p class="title">{{ title }}</p>
    <div class="form-control">
      <div class="form-checkbox" v-for="(item, index) in items" :key="index">
        <input type="checkbox" :name="item.key" @change="onChange(index)" />
        <p class="text-content">{{ item }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FilterUI",
  props: {
    title: {
      type: String,
      default: "default title",
    },
    items: {
      type: Object,
    },
  },
  methods: {
    onChange(value) {
      this.$emit("onChange", value);
    },
  },
};
</script>

<style scoped>
.filter {
  width: 240px;
  background-color: #f5f5f5;
  border-radius: 4px;
  padding: 12px;
  text-align: left;
  display: flex;
  flex-direction: column;
  grid-gap: 16px;
}

.title {
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
}

.text-content {
  font-size: 12px;
  line-height: 16px;
  font-weight: 400;
}

.form-control {
  display: flex;
  flex-direction: column;
  grid-gap: 20px;
}

.form-checkbox {
  display: flex;
  grid-gap: 12px;
}
</style>
