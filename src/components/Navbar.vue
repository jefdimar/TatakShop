<template>
  <div>
    <!-- Navbar -->
    <b-navbar toggleable="lg" type="dark" variant="dark" fixed="top">
      <b-navbar-brand>Tatak Shop</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#" @click.prevent="home">Home</b-nav-item>
          <b-nav-item href="#" v-if="isLoggedIn" @click.prevent="cart">Shopping Cart</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item href="#" @click.prevent="login" v-if="!isLoggedIn">Login</b-nav-item>
          <b-nav-item href="#" @click.prevent="register" v-if="!isLoggedIn">Register</b-nav-item>
          <b-nav-item-dropdown right v-if="isLoggedIn">
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em v-text="user"></em>
            </template>
            <b-dropdown-item href="#" @click.prevent="logout">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  methods: {
    home () {
      this.$router.push('/')
    },
    cart () {
      this.$router.push('/cart')
    },
    login () {
      this.$router.push('/login')
    },
    register () {
      this.$router.push('/register')
    },
    logout () {
      localStorage.clear()
      this.$store.commit('set_isloggedin', false)
    }
  },
  computed: {
    isLoggedIn () {
      return this.$store.state.isLoggedIn
    },
    user () {
      return this.$store.state.user
    }
  },
  created () {
    if (localStorage.access_token) {
      this.$store.commit('set_isloggedin', true)
      this.$store.commit('set_user', localStorage.user)
    } else {
      this.$store.commit('set_isloggedin', false)
    }
  }
}
</script>

<style>
</style>
