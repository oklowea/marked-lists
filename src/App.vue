<template>
  <div class="page" id="app">
    <div class="page__wrapper">
      <div class="page__item">
        <div class="lists">
          <ListItem
            v-for="list in lists" :key="list.id"
            @on-change-checkbox="onChangeCheckbox"
            @on-change-count="onChangeCount"
            @on-change-color="onChangeColor"
            @toggle="toggle"
            :list="list"/>
        </div>
      </div>
      <div class="page__item">
        <div v-for="list in lists" :key="list.id" class="card">
          <div class="card__title">{{ list.name }}</div>
          <div class="card__colors">
            <template v-for="item in list.items">
              <div
                v-if="item.count && item.checked" :key="item.id"
                class="card-color">
                <div
                  v-for="(x,index) in item.count" :key="index"
                  :style="{ background: item.color}"
                  @click="deleteCardColorItem(item.id, list.id)"
                  class="card-color__item">&nbsp;
                </div>
              </div>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ListItem from './components/list.vue';

export default {
  name: 'App',

  data() {
    return {
      lists: [
        {
          id: 1,
          name: 'List 1',
          items: [
            {
              id: 1, name: 'Item 1', checked: true, count: 10, color: '#ff0000',
            },
            {
              id: 2, name: 'Item 2', checked: true, count: 30, color: '#ffff00',
            },
            {
              id: 3, name: 'Item 3', checked: false, count: 40, color: '#00ff00',
            },
            {
              id: 4, name: 'Item 4', checked: false, count: 1, color: '#0000ff',
            },
          ],
        },
        {
          id: 2,
          name: 'List 2',
          items: [
            {
              id: 1, name: 'Item 1', checked: false, count: 1, color: '#ff0000',
            },
            {
              id: 2, name: 'Item 2', checked: true, count: 6, color: '#ffff00',
            },
            {
              id: 3, name: 'Item 3', checked: true, count: 3, color: '#00ff00',
            },
            {
              id: 4, name: 'Item 4', checked: false, count: 2, color: '#0000ff',
            },
          ],
        },
        {
          id: 3,
          name: 'List 3',
          items: [
            {
              id: 1, name: 'Item 1', checked: false, count: 3, color: '#ff0000',
            },
            {
              id: 2, name: 'Item 2', checked: false, count: 3, color: '#ffff00',
            },
            {
              id: 3, name: 'Item 3', checked: false, count: 3, color: '#00ff00',
            },
            {
              id: 4, name: 'Item 4', checked: false, count: 3, color: '#0000ff',
            },
          ],
        },
        {
          id: 4,
          name: 'List 4',
          items: [
            {
              id: 1, name: 'Item 1', checked: false, count: 4, color: '#ff0000',
            },
            {
              id: 2, name: 'Item 2', checked: false, count: 4, color: '#ffff00',
            },
            {
              id: 3, name: 'Item 3', checked: false, count: 4, color: '#00ff00',
            },
            {
              id: 4, name: 'Item 4', checked: false, count: 4, color: '#0000ff',
            },
          ],
        },
        {
          id: 5,
          name: 'List 5',
          items: [
            {
              id: 1, name: 'Item 1', checked: false, count: 5, color: '#ff0000',
            },
            {
              id: 2, name: 'Item 2', checked: false, count: 5, color: '#ffff00',
            },
            {
              id: 3, name: 'Item 3', checked: false, count: 5, color: '#00ff00',
            },
            {
              id: 4, name: 'Item 4', checked: false, count: 5, color: '#0000ff',
            },
          ],
        },
      ],
    };
  },

  components: {
    ListItem,
  },

  methods: {
    onChangeCheckbox(payload) {
      const list = this.lists.find((o) => o.id === payload.listId);
      const item = list.items.find((o) => o.id === payload.itemId);
      item.checked = payload.status;
    },

    onChangeCount(payload) {
      const list = this.lists.find((o) => o.id === payload.listId);
      const item = list.items.find((o) => o.id === payload.itemId);
      item.count = Number(payload.value);
    },

    onChangeColor(payload) {
      const list = this.lists.find((o) => o.id === payload.listId);
      const item = list.items.find((o) => o.id === payload.itemId);
      item.color = payload.value;
    },

    deleteCardColorItem(itemId, listId) {
      const list = this.lists.find((o) => o.id === listId);
      const item = list.items.find((o) => o.id === itemId);
      item.count -= 1;
    },

    toggle(listId) {
      const list = this.lists.find((o) => o.id === listId);
      const hasUnchecked = list.items.filter((o) => !o.checked).length;

      for (let i = 0; i < list.items.length; i += 1) {
        list.items[i].checked = hasUnchecked;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.page {
  width: 980px;
  margin: 0 auto;
  border: 1px solid #000;

  &__wrapper {
    display: flex;
    padding: 20px;
  }

  &__item {
    width: 50%;
    border: 1px solid #000;

    &:first-child {
      margin-right: 20px;
    }
  }
}

.lists {
  margin: 20px;
}

.card {
  border: 1px solid #000000;
  margin: 20px;
  padding: 8px;

  &__title {
    margin-bottom: 6px;
  }
}

.card-color {
  overflow: auto;
  margin-bottom: 4px;

  &:last-child {
    margin-bottom: 0;
  }

  &__item {
    float: left;
    width: 13px;
    height: 13px;
    margin-right: 4px;
    margin-bottom: 4px;
  }
}
</style>
