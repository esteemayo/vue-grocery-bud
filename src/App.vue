<template>
  <section class="section-center">
    <form class="grocery-form" @submit.prevent="handleSubmit">
      <Alert v-if="alert.show" :alert="alert" :hideAlert="showAlert" />
      <h3>Grocery Bud</h3>
      <div class="form-control">
        <input
          type="text"
          placeholder="e.g. Eggs"
          class="grocery"
          v-model="name"
          ref="inputRef"
        />
        <button type="submit" class="submit-btn">
          <span v-if="isEditing">Edit</span>
          <span v-else>Submit</span>
        </button>
      </div>
    </form>

    <div class="grocery-container" v-if="lists.length > 0">
      <List
        v-for="item in lists"
        :key="item.id"
        :item="item"
        :onEdit="editItem"
        :onDelete="deleteItem"
      />

      <button class="clear-btn" @click="clearList">Clear Items</button>
    </div>
  </section>
</template>

<script>
import items from '@/data';
import List from '@/components/List.vue';
import Alert from '@/components/Alert.vue';

export default {
  name: 'App',
  components: {
    List,
    Alert,
  },
  data() {
    return {
      lists: items,
      name: '',
      editID: null,
      isEditing: false,
      alert: {
        show: false,
        msg: '',
        type: '',
      },
    };
  },
  methods: {
    handleSubmit() {
      if (!this.name) {
        this.showAlert(true, 'danger', 'Please enter a value');
      } else if (this.name && this.editID) {
        this.lists = this.lists.map((item) =>
          item.id === this.editID ? { ...item, title: this.name } : item
        );

        this.name = '';
        this.editID = null;
        this.isEditing = false;

        this.showAlert(true, 'success', 'Value changed');
      } else {
        this.showAlert(true, 'success', 'Item added to the list');

        const newList = {
          id: new Date().getTime().toString(),
          title: this.name,
        };

        this.lists.push({ ...newList });
        this.name = '';
      }
    },
    showAlert(show, type, msg) {
      this.alert = { show, type, msg };
    },
    editItem(id) {
      const specificItem = this.lists.find((item) => item.id === id);

      this.isEditing = true;
      this.editID = specificItem.id;
      this.name = specificItem.title;
    },
    deleteItem(id) {
      this.showAlert(true, 'danger', 'Item removed');
      this.lists = this.lists.filter((item) => item.id !== id);
    },
    clearList() {
      this.showAlert('true', 'danger', 'Empty list');
      this.lists = [];
    },
  },
  mounted() {
    this.$refs.inputRef.focus();
  },
};
</script>

<style></style>
