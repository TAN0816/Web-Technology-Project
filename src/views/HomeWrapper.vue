<template>
  <div class="home-wrapper">
    <section>
      <div class="grid">
        <div class="content">
          <div class="content-left">
            <div class="info">
              <h2>Order Your Best Delicious Food</h2>
              <p>Hey, Our delicious food is waiting for you,<br>
                We are always near to you with fresh item of food
              </p>
            </div>
            <button @click="menu">Order Now!</button>
          </div>
          <div class="content-right">
            <img src="@/assets/image/plate.png" alt="dashboard pic">
          </div>
        </div>
      </div>
    </section>

    <div class="category">
      <div class="list-items">
        <h3>Popular Dishes</h3>
        <div class="card-list">
          <div class="card" v-for="(dish, index) in popularDishes" :key="index">
            <img :src="getImageUrl(dish.FoodImg)" :alt="dish.FoodName">
            <div class="food-title">
              <h1>{{ dish.FoodName }}</h1>
            </div>
            <div class="desc-food">
              <p>{{ dish.FoodDescription }}</p>
            </div>
            <div class="price">
              <span>RM{{ dish.FoodPrice }}</span>
              <span>
                <i class='bx bxs-star icon-col' v-for="star in dish.rating" :key="star"></i>
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeWrapper',
  data() {
    return {
      popularDishes: []
    };
  },
  methods: {
    menu() {
      window.location.href = "./login.php";
    },
    fetchPopularDishes() {
      fetch('http://localhost:8080/popular_dashboardfood')
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          this.popularDishes = data;
        })
        .catch(error => {
          console.error('There was an error fetching the popular dishes!', error);
        });
    },
    getImageUrl(imageName) {
      // return imgPath; // Ensure this path is accessible from the frontend
      return require('../assets/image/food/' + imageName)
    }
  },
  mounted() {
    this.fetchPopularDishes();
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;1,500&display=swap');

*{
  padding: 0;
  /*margin:0;
  box-sizing:border-box;
  font-family:'Poppins', sans-serif;*/
}

body{
  background: whitesmoke;
  
}

.wrapper{
  justify-content: center;
  align-items: center;
  min-height: 60vh;
  margin:0;
}

.nav{
  position:fixed;
  top:0;
  display:flex;
  justify-content:space-around;
  width:100%;
  height:100px;
  line-height:100px;
  z-index:100;
  background: #ffffff;
  margin:0;

}

.nav-logo p{
  color:rgb(255, 164, 170);
  font-size: 25px;
  font-weight: 600;
  margin:0;
}

.nav-logo b{
  color:rgb(30, 94, 88);
  margin:0;
}
.nav-menu ul{
  display:flex;
  margin:0;
  font-family:'Poppins', sans-serif;
}

.nav-menu ul li{
  list-style-type: none;
  margin:0;
  font-family:'Poppins', sans-serif;
}

.nav-menu ul li .link{
  text-decoration: none;
  font-weight: 500;
  color:black;
  padding-bottom: 15px;
  margin:0 25px;
  
  
}

.link:hover, .active{
  border-bottom:2px solid#fc6027;
  
}

.loginBtn, .registerBtn{
  width:130px;
  height:40px;
  font-weight:200;
  background:rgba(255, 232, 204, 0.6);
  color:black;
  border:none;
  border-radius:30px;
  cursor:pointer;
  transition: .3s ease;
   cursor: pointer;
  transition: .3s ease;
  display: inline-flex;
  justify-content: center;
  align-items: center; 
  
}

.loginBtn {
  margin-right: 10px;
}
.loginBtn:hover, .registerBtn:hover{
  background-color: #ff9a75;
}

#registerBtn{
  margin-left:15px;
}

.dropdown img, .dropdown p{
  width: 35px;
  display: inline;
  cursor: pointer;
}
.dropdown{
  display: flex;
  align-items: center;
  background-color: white;
  height: 100px;
  width: 100px;
  font-weight: 100;
  font-family:'Poppins', sans-serif;

}

.account{
  margin-right: 50px;
}
.dropdown-item{
  position: absolute;
  top: 70px;
  height: 0;
  width: 100px;
  z-index: 999;
  transition: height 0.3s linear;
  transition-delay: 0.1s;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background-color: rgb(255, 198, 164);
  border-radius: 10px;
  right: 140px;
}
.dropdown:hover .dropdown-item{
  transition: height 0.3s linear;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
  background-color: rgb(255, 198, 164);
  border-radius: 10px;
}
.customerlogout{
  text-decoration: none;
  color: black;
  
}



/*============CONTENT=========*/
.content{
  display:grid;
  grid-template-columns: 50% auto;
  gap:30px;
  margin: 120px 100px 50px 100px;
  align-items: center;
  justify-content: space-between;
  width:100;
}
/* =====Left-Size====== */
.content .content-left{
  display: block;
  width:100%;
}

.content .content-left .info{
  max-width:100%;
  display:flex;
  flex-direction: column;
}

.content .content-left .info h2{
  font-size:60px;
  font-family: sans-serif;
  margin-bottom:20px;
}

.content .content-left .info p{
  font-size: 23px;
  line-height: 2pc;
  margin-bottom:30px;
}


/*======Button===== =*/

.content  .content-left button{
  padding:10px 23px;
  background-color:#ff511c;
  color:#ffffff;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  width:130px;
  font-size: 100;
  font-family: sans-serif;
  display:block;
  margin:0px 250px;
}

.content button:hover{
  background: rgba(255, 163, 107, 0.671);
}


/*====RIGHT SIDE=====*/

.content .content-right{
  display:block;
  width:100%
}

.content .content-right img{
  width:450px;
  height:auto;
  position:relative;
  animation: rotate 10s linear infinite;
  border-radius: 400px;
}

/*===ANIMATION====*/

@keyframes rotate{
  0%{
    transform: rotate(0deg);
  }

  100%{
    transform: rotate(360deg)
  }
}


.category{
  width:100%;
  display:flex;
  margin-bottom:50px;
  margin-left:40px;
  margin-right:20px;
  justify-content:center;
}

.category .list-items{
  width:90%;
  position:relative;
  margin-top:0px;
  justify-content: center;
}

.category .list-items h3{
  font-size:20px;
  font-weight:600;
  font-family: sans-serif;
  margin-bottom:90px;
  padding-right:100px;
  text-align:left;

}

.category .list-items .card-list{
  display:grid;
  grid-template-columns: repeat(4, 1fr);
}

.category .card-list .card{
  width:200px;
  height:auto;
  display: block;
  padding:10px;
  border-radius:10px;
  position:relative;
  background:#ffffff;
  outline:2px solid #faad96;
}

.category .card-list .card img{
  width:100px;
  height:100px;
  bottom:225px;
  left:50px;
  object-fit:cover;
  object-position:center;
  background-repeat: no-repeat;
  position:absolute;
  box-shadow: 0 20px 20px #faad96;
  border-radius: 50%;
}

.category .card-list .card .food-title{
  padding: 40px 0 10px;
}

.category .card-list .card .food-title h1{
  text-align:center;
  font-weight: bold;
  font-size:16px;
  font-family: sans-serif;
}

.category .card-list .card .desc-food p{
  font-size: 13px;
  text-align: center;
  font-weight: 500;
  margin-bottom: 20px;
  font-family:sans-serif;
}

.category .card .price{
  /*display: flex;
  align-items: center;*/
  justify-content: space-between;

}

.category .card .price span{
  font-weight:600;
  font-family: sans-serif;
  
}

.category .card .price .icon-col{
  color:#ff511c;
  font-size: 20px;
  
}


/* scroll bar 
::-webkit-scrollbar{
  width:8px;
}

::-webkit-scrollbar-thumb{
  border-radius:10px;
  background-color:#ff511c;
}

*/
</style>
