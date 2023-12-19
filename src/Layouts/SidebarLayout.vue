<template>
  <div class="sidebar">
    <ul>
      <li @click="selectItem('About')">Shows</li>
      <li @click="selectItem('about')">Podcasts</li>
      <li @click="selectItem('Contact')">Contact</li>
    </ul>
  </div>
</template>
  
  <script>
  export default {
    name: 'SidebarLayout',
  };
  </script>
  
  <style scoped>
.sidebar {
  width: 200px;
  height: 100%;
  background-color: #212121;
  color: white;
  padding: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  cursor: pointer;
  padding: 8px;
  border-bottom: 1px solid #333;
}

li:hover {
  background-color: #333;
}
</style>
  