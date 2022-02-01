<template>
  <div class="grocery-list">
    <article class="grocery-item">
      <p class="title">{{ item.title }}</p>
      <div class="btn-container">
        <button class="edit-btn" @click="onEdit(item.id)">
          <i class="fas fa-edit"></i>
        </button>
        <button class="delete-btn" @click="onDelete(item.id)">
          <i class="fas fa-trash"></i>
        </button>
      </div>
    </article>
  </div>
</template>

<script>

export default {
  name: 'Lists',
  props: {
    item: Object,
    onEdit: Function,
    onDelete: Function,
  },
};
</script>

<style></style>
