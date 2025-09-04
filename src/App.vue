<template>
  <header>
    <nav>
      <ul>
        <li class = "nav-item">
          <router-link class="nav-link" :to="{name: 'Home'}" exact>
          <img class="logo" src="./assets/build-a-bot-logo.png">
          Build-a-Bot
          </router-link>  
        </li>
        <li class = "nav-item">
          <router-link class="nav-link" :to="{name: 'Build'}" exact>
          Build
          </router-link>  
        </li>        
        <li class = "nav-item cart">
          <router-link class="nav-link" to='/cart' exact>
          Cart
          </router-link>  
          <div class="cart-items" v-if="cart.length > 0">
            {{ cart.length }}
          </div>
        </li>             
      </ul>
    </nav>
  </header>
    <div class="container">
      <aside class="aside">
        <router-view name="sidebar"/>
      </aside>
      <main>
        <router-view/>
      </main>
    </div>
</template>

<script>
export default {
  name: "App",
  computed: {
    cart() {
      return this.$store.state.cart;
    }
  }
};
</script>

<style>
body {
  background: linear-gradient(to bottom, #2c3e50, #3498db);
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>

<style scoped>

main {
  padding: 30px;
  background-color: white;
  width: 964px;
  min-height: 300px;
}

header {
  background-color: #999;
  width: 1184px;
  margin: 0 auto;
}
ul {
  padding: 3px;
  display: flex;
}
.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1px solid #bbb;
}

.nav-item.cart {
  position: relative;
  margin-left: auto;
  border-right: none;
}

.logo {
  vertical-align: middle;
  height: 30px;
}

.nav-link {
  text-decoration: none;
  color: inherit;
}

.router-link-active {
  font-weight: bold;
  color: white;
}

.container {
  display: flex;
  margin: 10px, auto 0 auto;
  justify-content: center;
}
.aside {
  width: 100px;
  background-color: #eee;
  padding: 30px;
  min-height: 300px;
}
.cart-items {
  position: absolute;
  top: -10px;
  right: -10px;
  background-color: seagreen;
  color: white;
  border-radius: 12px;
  padding: 2px 6px;
  font-size: 12px;
}
</style>
