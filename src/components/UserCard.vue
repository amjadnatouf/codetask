<template>
  <div class="user-card">
    <div class="image-container">
      <img :src="user.avatar" alt="avatar" />
    </div>
    <div class="content">
      <div class="title">
        {{ user.first_name + " " + user.last_name }}
      </div>
      <a :href="`mailto:${user.email}`" class="email">contact</a>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  props: ["user"],
};
</script>

<style>
.user-card {
  border-radius: 10px;
  background-color: #f0f0f0;
  padding: 1rem 0;
  width: 140px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.image-container {
  width: 100px;
  height: 100px;
  border: 2px solid #00000061;
  padding: 2px;
  border-radius: 50%;
  margin: 0 1rem;
}

.image-container img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
}

.content {
  text-align: center;
  margin-top: 1rem;
  width: 100%;
}

.title {
  font-weight: bold;
  font-size: 15px;
  margin-bottom: 0.5rem;
}

.email {
  color: #666;
  text-decoration: none;
}
</style>
