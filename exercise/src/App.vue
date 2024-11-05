<script setup>
import { reactive, ref } from 'vue';
import UserForm from './components/UserForm.vue';
import UserCard from './components/UserCard.vue';

const users = ref([]);
const currentUser = ref(null);
const isEditing = ref(false);

const addUser = (user) => {
  if (isEditing.value) {
    // Update existing user
    const index = users.value.findIndex(u => u.id === currentUser.value.id);
    users.value[index] = { ...user, id: currentUser.value.id };
    isEditing.value = false;
    currentUser.value = null;
  } else {
    // Add new user
    users.value.push({ ...user, id: Date.now() });
  }
};

const editUser = (user) => {
  isEditing.value = true;
  currentUser.value = user;
};

const deleteUser = (userId) => {
  users.value = users.value.filter(user => user.id !== userId);
};
</script>

<template>
  <div class="container">
    <UserForm
      :isEditing="isEditing"
      :currentUser="currentUser"
      @submitForm="addUser"
    />
    <div class="user-list">
      <UserCard
        v-for="user in users"
        :key="user.id"
        :user="user"
        @edit="editUser"
        @delete="deleteUser"
      />
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 80%;
  margin: auto;
}
.user-list {
  display: flex;
  flex-wrap: wrap;
}
.user-card {
  margin: 10px;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  width: 200px;
}
.user-form {
  margin-bottom: 20px;
}
</style>
