<template>
    <form @submit.prevent="handleSubmit" class="row g-3 container-fluid px-5 my-5">
      <div class="col-md-6">
        <label class="form-label">First Name</label>
        <input type="text" class="form-control" v-model="formData.firstName" required />
      </div>
      <div class="col-md-6">
        <label class="form-label">Last Name</label>
        <input type="text" class="form-control" v-model="formData.lastName" required />
      </div>
      <div class="col-md-12">
        <label class="form-label">Address</label>
        <input type="text" class="form-control" v-model="formData.address" required />
      </div>
      <div class="col-md-6">
        <label class="form-label">Email</label>
        <input type="email" class="form-control" v-model="formData.email" required />
      </div>
      <div class="col-md-6">
        <label class="form-label">Mobile Number</label>
        <input type="text" class="form-control" v-model="formData.mobilenumber" required />
      </div>
      <div class="col-md-12">
        <label class="form-label">Upload Image</label>
        <input type="file" class="form-control" @change="handleImageUpload" accept="image/*" />
      </div>
      <div class="d-flex justify-content-end">
        <button type="submit">{{ isEditing ? 'Update' : 'Add' }} User</button>
      </div>
    </form>
  </template>
  
  <script>
  import { reactive, watch } from 'vue';
  
  export default {
    props: {
      isEditing: Boolean,
      currentUser: Object
    },
    setup(props, { emit }) {
      const formData = reactive({
        firstName: '',
        lastName: '',
        address: '',
        email: '',
        mobilenumber: '',
        image: null
      });
  
      watch(
        () => props.currentUser,
        (newVal) => {
          if (newVal) {
            Object.assign(formData, newVal);
          }
        },
        { immediate: true }
      );
  
      const handleImageUpload = (event) => {
        const file = event.target.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = (e) => {
            formData.image = e.target.result;
          };
          reader.readAsDataURL(file);
        }
      };
  
      const handleSubmit = () => {
        emit('submitForm', { ...formData });
        Object.keys(formData).forEach(key => formData[key] = '');
      };
  
      return { formData, handleSubmit, handleImageUpload };
    }
  };
  </script>
  