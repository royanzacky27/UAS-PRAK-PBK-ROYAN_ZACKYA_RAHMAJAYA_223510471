<template>
  <nav class="navbar">
    <div class="navbar-brand">
      <router-link to="/" class="navbar-item">WEATHER</router-link>
    </div>
    <div class="task-links">
      <div class="dropdown" @click="toggleDropdown">
        <div class="navbar-item">Tugas Royan Zackya Rahmajaya ⬇</div>
        <div class="dropdown-menu" :class="{ 'is-active': isDropdownActive }">
          <a href="https://royan-project-cv.web.app/" class="navbar-item" target="_blank">TUGAS 1</a>
          <a href="https://royanzacky-tugas2.web.app/" class="navbar-item" target="_blank">TUGAS 2</a>
          <a href="https://royan-t3-223510471.web.app/" class="navbar-item" target="_blank">TUGAS 3</a>
          <a href="https://tugas4-pbk-omega.vercel.app/" class="navbar-item" target="_blank">TUGAS 4</a>
          <a href="https://github.com/royanzacky27/T4_223510471_royanzackyarahmajaya_4G" class="navbar-item" target="_blank">TUGAS 5</a>
          <a href="" class="navbar-item" target="_blank">TUGAS 6</a>
          <a href="https://royanzackyarahmajaya223510471tugas7-7c8wtdhlk.vercel.app/" class="navbar-item" target="_blank">TUGAS 7</a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      isDropdownActive: false
    };
  },
  methods: {
    toggleDropdown() {
      this.isDropdownActive = !this.isDropdownActive;
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap');

.navbar {
  background-color: #343a40; /* Dark grey background */
  color: #f8f9fa; /* Light grey text */
  padding: 15px 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: 'Roboto', sans-serif; /* Using Roboto font */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Adding shadow for depth */
}

.navbar-brand {
  display: flex;
  align-items: center;
}

.navbar-item {
  color: #f8f9fa;
  text-decoration: none;
  margin: 0 15px;
  padding: 10px 15px;
  border-radius: 8px;
  transition: background-color 0.3s, color 0.3s;
  font-size: 18px;
}

.navbar-item:hover {
  background-color: #495057;
  color: #f8f9fa;
}

.task-links {
  display: flex;
  align-items: center;
}

.dropdown {
  position: relative;
  cursor: pointer;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: calc(100% + 10px);
  left: 50%;
  transform: translateX(-50%);
  background-color: #212529; /* Darker grey background */
  border-radius: 8px;
  padding: 10px 0;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  width: 220px;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

.dropdown-menu.is-active {
  display: block;
  opacity: 1;
  pointer-events: auto;
}

.dropdown-menu .navbar-item {
  display: block;
  width: 100%;
  padding: 10px 20px;
  font-size: 16px;
}

.dropdown-menu .navbar-item:hover {
  background-color: #495057;
}

.navbar-item.active {
  background-color: #495057;
}
</style>
