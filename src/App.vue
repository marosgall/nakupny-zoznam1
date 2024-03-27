<template>
  <h1>Shopping list</h1>
  <h3>New item</h3>
  <input class="textInput" v-model="itemName" type="text" autofocus>
  <button @click="addItem()">Add to list</button>
  <hr>
  <h2>Items</h2>
  <ul>
    <li v-for="item in validItems" :key="item.id">
      <span class="delButton" @click="deleteItem(item)">x</span>
      {{ item.text }}
    </li>
  </ul>
  <hr>
  <h2>Deleted items</h2>
  <ul>
    <li v-for="item in deletedItems" :key="item.id">
      <p class="deleted">{{ item.text }}</p>
    </li>
  </ul>
</template>

<script>
  export default {
    data() {
      return {
        itemName: '',
        items: []
      }
    },
    methods: {
      addItem() {
        this.items.push({
          id: this.items.length + 1,
          text: this.itemName,
          is_deleted: false
        })

        console.log(this.itemName)
        this.itemName = ''
      },
      deleteItem(item) {
        item.is_deleted = true
        console.log(`${item.text} is deleted: ${item.is_deleted}`)
      }
    },
    computed: {
      validItems() {
        return this.items.filter(item => !item.is_deleted) 
      },
      deletedItems() {
        return this.items.filter(item => item.is_deleted)
      }
    },
  }
</script>
