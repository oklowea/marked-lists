<template>
  <div class="list">
    <div class="list__title">
      <div
        @click="toggle"
        class="list__check"
        :class="{'list__check--point': isPoint, 'list__check--mark': isMark}">
      </div>
      <label @click="isOpen = !isOpen">
        <span>{{ list.name }}</span>
      </label>
    </div>
    <div v-if="isOpen" class="list__items">
      <lineItem
        v-for="item in items" :key="item.id"
        @on-change-checkbox="onChangeCheckbox"
        @on-change-count="onChangeCount"
        @on-change-color="onChangeColor"
        :item="item" />
    </div>
  </div>
</template>

<script>
import lineItem from './line.vue';

export default {
  name: 'List',

  components: {
    lineItem,
  },

  props: {
    list: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      isOpen: Boolean(this.list.items.filter((o) => o.checked).length),
      items: this.list.items,
    };
  },

  computed: {
    isPoint() {
      const hasChecked = Boolean(this.list.items.filter((o) => o.checked).length);
      const hasUnchecked = Boolean(this.list.items.filter((o) => !o.checked).length);

      return hasChecked && hasUnchecked;
    },

    isMark() {
      const hasUnchecked = Boolean(this.list.items.filter((o) => !o.checked).length);

      return !hasUnchecked;
    },
  },

  methods: {
    onChangeCheckbox(payload) {
      this.$emit('on-change-checkbox', {
        ...payload,
        listId: this.list.id,
      });
    },

    onChangeCount(payload) {
      this.$emit('on-change-count', {
        ...payload,
        listId: this.list.id,
      });
    },

    onChangeColor(payload) {
      this.$emit('on-change-color', {
        ...payload,
        listId: this.list.id,
      });
    },

    toggle() {
      this.$emit('toggle', this.list.id);
    },
  },
};
</script>

<style lang="scss" scoped>
.list {
  &__title {
    display: flex;
    margin-bottom: 6px;
  }

  &__check {
    border: 1px solid #000;
    width: 14px;
    height: 14px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-right: 10px;

    &--point {
      &:before {
        content: '\2022';
      }
    }

    &--mark {
      &:before {
        content: '\2713';
      }
    }
  }
  &__items {
    padding: 0 20px;
  }
}
</style>
