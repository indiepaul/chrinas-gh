
<template>
  <header class="header" :class="{sticky: $route.path === '/' || $route.path.includes('/blogs/')}">
    <div class="container">
      <div class="left">
        <g-link :to="{ name: 'home' }" class="home-link">
          <img src="../../static/logo.svg" :alt="settings.site_name" class="logo">
        </g-link>
      </div>
      <nav id="nav" class="nav right">
        <a class="icon toggle" @click="toggle">
          <i class="fa fa-bars"></i> Menu
        </a>
        <div id="links">
          <g-link class="nav__link" to="/" exact>Home</g-link>
          <g-link class="nav__link" to="/about">About us</g-link>
          <g-link class="nav__link cta" to="/reservations">Reservations</g-link>
          <g-link class="nav__link" to="/explore">Explore</g-link>
          <g-link class="nav__link" to="/house-rules">House Rules</g-link>
          <g-link class="nav__link" to="/contact">Contact Us</g-link>
        </div>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      logo: require("../../static/logo.svg"),
      settings: require("../../data/theme.json")
    };
  },
  methods: {
    toggle() {
      var x = document.getElementById("links");
      if (x.style.display === "block") {
        x.style.display = "none";
      } else {
        x.style.display = "block";
      }
    }
  }
};
</script>

<style scoped>
.header {
  position: relative;
  height: 6rem;
  z-index: 10;
  background-color: white;
}
.header.sticky {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
.header > .container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
.home-link {
  text-decoration: none;
}
.logo {
  height: 1.5rem;
}
.site-name {
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  text-decoration: none;
  text-transform: uppercase;
}
#links > * {
  font-size: 0.9rem;
  font-weight: 600;
  text-decoration: none;
  margin-top: 4px;
  margin-right: 3rem;
  padding-bottom: 4px;
  border-bottom: 1px solid;
  border-color: transparent;
  transition: border 0.15s;
}
#links > *:last-of-type {
  margin: 0;
}
#links > *:hover {
  border-color: var(--theme-color);
}
#links > .active {
  border-color: var(--theme-color);
}
.cta {
  background-color: var(--theme-color);
  border-radius: 30px;
  padding: 0.5rem 0.5rem 0.9rem 0.5rem;
}
nav .toggle {
  display: none;
}
@media (max-width: 644px) {
  .header.sticky {
    position: static;
  }
  .layout.sticky-header {
    padding: 0rem 0 0 0;
  }
  #links .nav__link {
    display: block;
    width: 100vw;
    text-decoration: none;
    border-bottom: 1px solid black;
    padding: 14px 16px;
  }
  #links {
    position: relative;
    margin-top: 15rem;
    margin-right: 3rem;
    overflow: hidden;
    display: none;
    background-color: white;
  }
  nav .toggle {
    display: block;
    position: absolute;
    top: 35px;
    right: 50px;
    z-index: 100;
  }

  .cta {
    border-radius: 0;
  }
}
</style>
