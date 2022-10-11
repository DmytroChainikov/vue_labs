<template>
  <div class="home pa-6">
    <v-text-field
      outlined
      label="Add new item"
      append-icon="mdi-cart-plus"
      clearable
      v-model="newItemTitle"
      @click:append="addNewItem"
      @keyup.enter="addNewItem"
    />
    <v-list
      subheader
      flat
    >

      <div
        v-for="item in shoppingList"
        :key="item.id"
      >
        <v-list-item
          @click="doneBought(item.id)"
          :class="{ 'blue lighten-5' : item.bought }"
        >
          <template>
            <v-list-item-action>
              <v-checkbox
                :input-value="item.bought"
                color="primary"
              />
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through' : item.bought }"
              >
                {{ item.title }}
              </v-list-item-title>
            </v-list-item-content>

            <div class="v-list-item__action">
              <button
                type="button"
                class="v-btn v-btn--icon v-btn--round theme--light v-size--default"
                @click.stop="deleteItem(item.id)"
              >
                <span class="v-btn__content">
                  <i
                    aria-hidden="true"
                    class="v-icon notranslate mdi mdi-delete theme--light grey--text text--lighten-1"
                  />
                </span>
              </button>
            </div>
          </template>
        </v-list-item>
        <v-divider />
      </div>

    </v-list>
  </div>
</template>

<script>
export default {
  name: 'ListView',
  data: () => ({
    shoppingList: [
      { id: 1, title: 'One', bought: false },
      { id: 2, title: 'Two', bought: false },
      { id: 3, title: 'Three', bought: false }
    ],
    newItemTitle: ''
  }),
  components: {
  },
  methods: {
    doneBought (id) {
      const item = this.shoppingList.filter(item => item.id === id)[0]
      item.bought = !item.bought
    },
    deleteItem (id) {
      this.shoppingList = this.shoppingList.filter(item => item.id !== id)
    },
    addNewItem () {
      const newItem = {
        id: Date.now(),
        title: this.newItemTitle,
        bought: false
      }
      this.shoppingList.push(newItem)
      this.newItemTitle = ''
    }
  }
}
</script>
