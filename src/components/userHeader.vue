<template>
  <nav class="navigation-bar">
    <div class="nav-logo">
      <p>Food.io</p>
    </div>

    <div class="nav-menu">
      <ul>
        <!-- Replace anchor tags with router-link -->
        <li><router-link to="/home" class="link" :class="{ active: isActive('/home')}" >Home</router-link></li>
        <li>
          <router-link to="/user/MenuCart" class="link" :class="{ active: isActive('/user/MenuCart')}">
            Menu & <i class="bx bx-cart"></i> Cart
          </router-link>
        </li>
        <li><router-link to="/user/order" class="link" :class="{ active: isActive('/user/order')}">Order</router-link></li>
      </ul>
    </div>

    <div class="account">
      <div class="dropdown">
        <img src="../assets/image/login.png" alt="login-pic" @click="goToProfile" />
        <p @click="goToProfile"><span style="text-decoration: none; color: black;">Customer</span></p>
        <div class="dropdown-item">
          <button class="customerlogout" @click="logout"><i class="bi bi-box-arrow-left"></i><span>Log Out</span></button>
        </div>
      </div>
    </div>
  </nav>
</template>

  
<script>
export default {
  methods: {
    goToProfile() {
      this.$router.push('/profile');
    },
    logout() {
      localStorage.removeItem('role');
      localStorage.removeItem('userid');
      window.location.href = '/login';
    },
    isActive(route) {
      return this.$route.path === route;
    }
  },
};
</script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;1,500&display=swap');
  
  * {
    padding: 0;
    box-sizing: border-box;
  }
  
  .navigation-bar {
    position: fixed;
    top: 0;
    display: flex;
    justify-content: space-around;
    width: 100%;
    height: 100px;
    line-height: 100px;
    z-index: 100;
    background: #ffffff;
    margin: 0;
  }
  
  .nav-logo p {
    color: rgb(255, 164, 170);
    font-size: 25px;
    font-weight: 600;
    margin: 0;
  }
  
  .nav-menu ul {
    display: flex;
    margin: 0;
    font-family: 'Poppins', sans-serif;
  }

  .nav-menu ul li {
    list-style-type: none;
    margin: 0;
    font-family: 'Poppins', sans-serif;
  }
  
  .nav-menu ul li .link {
    text-decoration: none;
    font-weight: 500;
    color: black;
    padding-bottom: 15px;
    margin: 0 25px;
  }
  
  .link:hover,
  .active {
    border-bottom: 2px solid #fc6027;
  }
  
  .dropdown img,
  .dropdown p {
    width: 35px;
    display: inline;
    cursor: pointer;
    margin-bottom:0%;
  }
  
  .dropdown {
    display: flex;
    align-items: center;
    background-color: white;
    height: 100px;
    width: 100px;
    font-weight: 100;
    font-family: 'Poppins', sans-serif;
  }
  
  .account {
    margin-right: 50px;
    position: relative;
  }
  
  .dropdown-item {
    position: absolute;
    top: 65px;
    height: 0;
    width: 110px;
    z-index: 999;
    transition: height 0.3s linear;
    transition-delay: 0.1s;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background-color: rgb(255, 198, 164);
    border-radius: 10px;
    right: -15px;
  }
  
  .dropdown:hover .dropdown-item {
    transition: height 0.3s linear;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 50px;
    background-color: rgb(255, 198, 164);
    border-radius: 10px;
  }
  
  .customerlogout {
    text-decoration: none;
    color: black;
    border: none;
    background: transparent;
  }
  </style>
  