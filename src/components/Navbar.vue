<template>
  <div class="container-flex">
    <nav class="navbar navbar-light">
      <div class="dropdown d-xl-none d-lg-none mr-auto">
        <img src="@/assets/list.svg" data-toggle="dropdown" data-target="#navd" aria-haspopup="true" aria-expanded="false">
        <div class="dropdown-menu hb" aria-labelledby="navd">
          <router-link class="dropdown-item" to="/">Home</router-link>
        </div>
      </div>
      <!--Header navigation-->
      <span class="navbar-item bc d-none d-xl-block d-lg-block py-0">
        <router-link class="pl-5" to="/">Home</router-link>
      </span>
      <div class="navbar-item ml-auto d-flex">
        <div class="searc d-none d-xl-block d-lg-block pr-3">
          <input type="search" class="search">
        </div>
        <div class="navbar-item bc user" v-if="isLoggedIn === false">
          <router-link to="/login"><h5 style="cursor: pointer">Login</h5></router-link>
        </div>
        <div class="navbar-item bc user" v-if="isLoggedIn === false">
          <router-link to="/register"><h5 style="cursor: pointer">Register</h5></router-link>
        </div>
        <div class="navbar-item bc user" v-if="isLoggedIn === true">
          <h5 style="cursor: pointer" @click="logout">Sign Out</h5>
        </div>

        <div class="bag" @click="openCart">
            <img class="pb-1" src="@/assets/cart.svg">
            <span class="mb-3" v-if="this.bagItemscount > 0">{{ bagItemscount }}</span>
        </div>
      </div>
    </nav>
    <!--Cart Component-->
    <Cart ref="cartMove" />
  </div>
</template>

<script>
import Cart from './Cart.vue'

export default {
  name: 'Navbar',
  components: {
    Cart
  },
  computed: {
    bagItemscount () {
      return this.$store.getters.itemsNumber
    },
    isLoggedIn () {
      return this.$store.state.isLoggedIn
    }
  },
  methods: {
    logout () {
      localStorage.clear()
      this.$store.commit('SET_LOGINSTATUS', false)
      this.$router.push('/')
    },
    openCart () {
      this.$refs.cartMove.cartON()
    }
  },
  created () {
    if (localStorage.getItem('access_token')) {
      this.$store.commit('SET_LOGINSTATUS', true)
    }
  }
}
</script>

<style>
nav {
  z-index:100;
}
.navbar {
  border-bottom: 1px solid #DCDCDC;
  background-color: #F8F8F8;
}

.close {
  position:relative;
  bottom:20px;
  left:10px;
  font-size: 31px;
  color: #000;
}

.dropdown img {
  height: 30px;
  width: 30px;
}

.navbar-item.bc a {
  font-size: 17px;
  text-decoration: none;
  color: black;
}

.navbar-item.bc a:hover, .navbar-item.bc a:active {
  color: #FFD700;
}
.btn-sm{
  border-radius: 0;
}

.search {
  outline: none;
  border: 1px #F8F8F8;
  background: #ededed url('../assets/search.png') no-repeat 5px center;
  padding: 5px 8px 0px 26px;
  width: 10px;
  -webkit-border-radius: 10em;
  -moz-border-radius: 10em;
  border-radius: 10em;
  -webkit-transition: all .5s;
  -moz-transition: all .5s;
  transition: all .5s;
  margin-right: 10px;
}

.search:focus {
  width: 160px;
  border: solid 1px #ccc;
  background-color: #fff;
  border-color: #98ccfd;
  -webkit-box-shadow: 0 0 5px rgba(109, 207, 246, .5);
  -moz-box-shadow: 0 0 5px rgba(109, 207, 246, .5);
  box-shadow: 0 0 5px rgba(109, 207, 246, .5);
  backface-visibility: hidden;
  perspective: 1000;
}

form .btn-xl.btn-success.mt-3 {
  position: relative;
  -webkit-transition-duration: 100ms;
  transition-duration: 100ms;
  width: 100%;
  height: 50px;
  font-size: 20px;
  outline:none;
  cursor: pointer;
  box-shadow: 0 26px 38px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.bag span {
    background-color: #6394F8;
    border-radius: 10px;
    color: white;
    position: absolute;
    font-size: 15px;
    line-height: 1;
    padding: 2px 3px 3px 3px;
    text-align: center;
    vertical-align: middle;
    white-space: nowrap;
    margin-left: -9px;
    bottom: 1rem;
}

.bag img {
  cursor: pointer;
  width: 30px;
  height: auto;
}

.user{
  margin-right: 20px;
  padding-top: 10px;
}

.user:hover {
  text-decoration: underline;
}

</style>
