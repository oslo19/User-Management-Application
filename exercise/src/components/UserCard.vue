<template>
    <div class="card user-card" style="width: 18rem;">
      <img v-if="user.image" :src="user.image" class="card-img-top" alt="User Image" />
      <div class="card-body">
        <h5 class="card-title">{{ user.firstName }} {{ user.lastName }}</h5>
        <p class="card-text">{{ user.address }}</p>
        <p class="card-text">{{ user.email }}</p>
        <p class="card-text">{{ user.mobilenumber }}</p>
        <div class="d-flex justify-content-between">
        <button class="btn btn-primary" @click="$emit('edit', user)">Edit</button>
        <button class="btn btn-danger" @click="$emit('delete', user.id)">Delete</button>
    </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      user: Object
    }
  };
  </script>
  
  <style scoped>
  .user-card {
    margin: 10px;
  }
  </style>
  