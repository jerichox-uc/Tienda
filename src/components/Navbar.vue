<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="container">
      <!-- Brand -->
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item">{{ brand }}</router-link>
        <a
          role="button"
          class="navbar-burger burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarMenu"
          :class="{ 'is-active': displayMenu }"
          @click="displayMenu = !displayMenu"
        >
        <img src="https://i.ibb.co/y45tnG6/Logo-te-asisto.png" alt="TeAsisto" width="112" height="28">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <!--  -->
      <div
        id="navbarMenu"
        class="navbar-menu"
        :class="{ 'is-active': displayMenu }"
      >
        <div class="navbar-start">
          <!--
          <a class="navbar-item">
            Home
          </a>
          -->
        </div>

        <div class="navbar-end">
          <a class="navbar-item cart" @click="showCart">
            <span class="icon">
              <i class="mdi mdi-32px mdi-cart"></i>
              <span
                class="tag is-warning"
                v-if="$store.getters.shoppingCart.list.length > 0"
                >{{ $store.getters.shoppingCart.list.length }}</span
              >
            </span>
          </a>
          <router-link class="navbar-item" to="/create"
            >Crear Producto</router-link
          >

          <router-link
            v-if="!isLoggedIn"
            to="/login"
            id="login"
            class="navbar-item"
            >Login</router-link
          >
          <div v-else class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link">
              <span class="icon">
                <i class="mdi mdi-32px mdi-account"></i>
              </span>
              Usuario
            </a>

            <div class="navbar-dropdown">
          <router-link class="navbar-item" to="/about"
            >Nosotros</router-link
          >

              <a class="navbar-item" @click="showCart">Ver Carrito</a>
              <hr class="navbar-divider" />
              <a class="navbar-item" @click="logout">Cerrar Sesión</a>
            </div>
          </div>
        </div>
      </div>
      <!--  -->
    </div>
    <!-- container -->
  </nav>
</template>

<script>
import { mapActions } from "vuex";
import firebase from "firebase";

export default {
  name: "",
  components: {},
  props: {
    brand: {
      type: String,
      default: "My-Store",
    },
  },
  data() {
    return {
      displayMenu: false,
    };
  },
  methods: {
    ...mapActions([]),
    showCart(event) {
      event.preventDefault();
      this.$store.dispatch("updateShowCart", true);
    },
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.push("/login");
          this.$store.dispatch("updateUser", false);
        });
    },
  },
  computed: {
    /* displayMenuStyle() {
      return { display: this.displayMenu ? "block" : "none" };
    }, */
    isLoggedIn() {
      return this.$store.getters.isLoggedIn;
    },
  },
  watch: {},
  created() {},
  mounted() {},
};
</script>

<style lang="scss" scoped>
nav {
  height: 4rem;
  background-color: #F4FA58;
}
</style>