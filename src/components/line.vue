<template>
  <div class="line">
    <label>
      <input type="checkbox" v-model="isChecked">
      <span>{{ item.name }}</span>
    </label>
    <div>
      <input type="text" v-model="count">
      <input type="color" v-model="color">
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      isChecked: this.item.checked,
      count: this.item.count,
      color: this.item.color,
    };
  },

  watch: {
    // eslint-disable-next-line
    'item.count'(value) {
      this.count = value;
    },

    // eslint-disable-next-line
    'item.checked'(value) {
      this.isChecked = value;
    },

    isChecked(status) {
      this.$emit('on-change-checkbox', {
        status,
        itemId: this.item.id,
      });
    },

    count(value) {
      this.$emit('on-change-count', {
        value,
        itemId: this.item.id,
      });
    },

    color(value) {
      this.$emit('on-change-color', {
        value,
        itemId: this.item.id,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.line {
  display: flex;
  justify-content: space-between;
  margin-bottom: 6px;

  label {
    input[type='checkbox'] {
      margin-right: 15px;
    }
  }

  input[type='text'] {
    width: 20px;
    border: none;
    border-color: transparent;
  }

  input[type='color'] {
    width: 20px;
    height: 20px;
    border-width: 0;
    padding: 0;
    background: transparent;

    &::-webkit-color-swatch {
      border-color: transparent;
    }
  }
}
</style>
