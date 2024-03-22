<template>
  <h1>Shopping list</h1>
  <label for="">New item</label><br>
  <input v-model="input" type="text" autofocus>
  <button @click="addItem()">Add to list</button>
  <hr>
  <h2>Items</h2>
  <ul>
    <li v-for="item in validItems" :key="`item-${item.id}`">
      <span @click="deleteItem(item)" style="margin-right: 15px;">x</span>
      {{ item.text }}
    </li>
  </ul>
  <hr>
  <h2>Deleted items</h2>
  <ul>
    <li v-for="item in deletedItems" :key="`item-${item.id}`">
      <p class="deleted">{{ item.text }}</p>
    </li>
  </ul>
</template>

<script>
  export default {
    data() {
      return {
        input: '',
        list: []
      }
    },
    methods: {
      addItem() {
        this.list.push({
          id: this.list.length + 1,
          text: this.input,
          is_deleted: false
        })

        console.log(this.input)
        this.input = ''
      },
      deleteItem(item) {
        item.is_deleted = true
        console.log(`${item.text} is deleted: ${item.is_deleted}`)
      }
    },
    computed: {
      validItems() {
        return this.list.filter(item => !item.is_deleted) 
      },
      deletedItems() {
        return this.list.filter(item => item.is_deleted)
      }
    },
  }
</script>

<style scoped>
  h2, ul, button {
    margin-bottom: 15px;
  }

  input {
    margin: 10px 0;
  }

  .deleted {
    text-decoration: line-through;
  }
</style>
