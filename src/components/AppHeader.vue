<script>
import { store } from "../js/store.js";
import { RouterLink } from "vue-router";

export default {
  name: "AppHeader",
  data() {
    return {
      isHidden: true,
      store,
      isModalOpened: false,
    };
  },
  computed: {
    cartCount() {
      return this.store.cartCount;
    },
  },
};
</script>
<template>
  <nav
    class="d-flex align-items-center justify-content-between p-1"
    :class="{ 'opened-modal': isModalOpened }"
  >
    <!-- Logo -->
    <div class="d-flex align-items-center">
      <RouterLink to="/">
        <img src="../assets/imgs/logo.jpeg" alt="logo" />
      </RouterLink>

      <RouterLink to="/">
        <h1 class="text-decoration-none d-none d-md-block ms-2">DeliveBoo</h1>
      </RouterLink>
    </div>

    <!-- Sezione Link -->
    <div class="nav-link">
      <RouterLink to="/">Home</RouterLink>

      <RouterLink to="/carrello" class="cart-box">
        <font-awesome-icon icon="cart-shopping" />
        <!-- conteggio degli articoli -->
        <span v-if="cartCount > 0" class="badge bg-danger cart-count">{{
          cartCount
        }}</span>
      </RouterLink>

      <button
        type="button"
        data-bs-toggle="modal"
        data-bs-target="#staticBackdrop"
        @click="isModalOpened = true"
      >
        Sei un Ristoratore?
      </button>
    </div>

    <!-- Modale -->
    <div
      class="modal fade"
      id="staticBackdrop"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      tabindex="-1"
      aria-labelledby="staticBackdropLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-body">
            <button type="button" class="log-btn m-3">
              <a href="http://127.0.0.1:8000/login">Accedi al tuo ristorante</a>
            </button>
            <button type="button" class="log-btn m-1">
              <a href="http://127.0.0.1:8000/register"
                >Registra il tuo ristorante</a
              >
            </button>
            <button
              type="button"
              class="close-btn"
              data-bs-dismiss="modal"
              @click="isModalOpened = false"
            >
              Chiudi
            </button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped lang="scss">
// Stile Navbar
nav {
  height: 100px;
  background-color: #fc7a1e;
  box-shadow: 0 0 10px rgba(94, 44, 3, 0.7);
  position: sticky;
  top: 0;
  left: 0;
  z-index: 1;

  &.opened-modal {
    position: initial;
  }

  a {
    text-decoration: none;
  }

  img {
    height: 80px;
    transition: scale 150ms;
  }

  img:hover {
    scale: (1.2);
  }

  h1 {
    margin-left: 20px;
    display: inline;
    vertical-align: middle;
    color: #faf6f6;
    font-weight: 700;
    text-decoration: underline;
  }

  .cart-box {
    position: relative;

    .cart-count {
      position: absolute;
      top: 0;
      right: 0;
      padding: 5px 8px;
      font-size: 10px;
      background-color: red;
      color: white;
      border-radius: 50%;
      transform: translate(85%, -65%);
    }
  }
}

// Sezione Link
.nav-link {
  * {
    margin-right: 20px;
    text-decoration: none;
    color: #faf6f6;
    font-size: 1.2rem;
    font-weight: 700;
  }
}

button {
  border: 1px;
  padding: 5px;
  border-radius: 12px;
  display: inline;
  background-color: #f24c00;
  color: #faf6f6;
  box-shadow: 0 0 10px rgba(94, 44, 3, 0.7);
}

.log-btn {
  background-color: #f24c00;
}

.close-btn {
  background-color: red;
  margin-left: 15px;
  text-align: center;
}

a {
  text-decoration: underline;
  color: #faf6f6;
}
</style>
