<template>
  <nav>
    <ul class="desktop-nav">
      <li>
        <nuxt-link to="/">
          <img src="https://www.byuradio.org/Content/site/logo.png" />
        </nuxt-link>
      </li>
      <nuxt-link v-for="(item, index) in navLinks" :key="index" :to="item.url">
        <li>{{item.label}}</li>
      </nuxt-link>
    </ul>

    <div class="mobile-nav">
      <nuxt-link to="/">
        <img src="https://www.byuradio.org/Content/site/logo.png" @click="logoClick" />
      </nuxt-link>
      <img
        @click="navToggle"
        src="https://cdn4.iconfinder.com/data/icons/navigation-40/24/hamburger-menu-512.png"
        alt="hamburger menu"
      />
    </div>

    <div class="mobile-sidebar" id="sidebar">
      <ul>
        <nuxt-link v-for="(item, index) in navLinks" :key="index" :to="item.url">
          <li @click="navToggle">{{item.label}}</li>
        </nuxt-link>
      </ul>
    </div>
  </nav>
</template>
<script>
export default {
  components: {},
  data: function () {
    return {
      navLinks: [
        {
          label: "Stations",
          url: "/stations",
        },
        {
          label: "Listen Live!",
          url: "/listen",
        },
      ],

      navOpen: false,
    };
  },

  methods: {
    navToggle() {
      console.log("nav toggled");
      var sidebar = document.getElementById("sidebar");
      sidebar.classList.toggle("open");
    },
    logoClick() {
      console.log("nav toggled");
      var sidebar = document.getElementById("sidebar");
      sidebar.classList.remove("open");
    },
  },
};
</script>


<style lang="scss" scoped>
nav {
  width: 100vw;
  height: 70px;
  background: white;
  position: fixed;
  top: 0;
  z-index: 9999;
  border-bottom: 1px solid black;

  img {
    height: 60px;
    width: auto;
  }
  .desktop-nav {
    ul {
      list-style-type: none;
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      display: flex;
      a {
        text-decoration: none;
        color: black;
      }
      li {
        height: 100%;
        max-width: 150px;
        min-width: 150px;
        //   background: blue;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: 0.1s ease-in-out;
        font-weight: bold;
        cursor: pointer;
      }
      li:hover {
        background: rgba(235, 235, 235, 0.603);
      }
    }
  }

  .mobile-nav {
    visibility: hidden;
  }

  .mobile-sidebar {
    * {
      visibility: hidden;
    }
  }
}

@media only screen and (max-width: 624px) {
  .desktop-nav {
    display: none;
  }
  .mobile-nav {
    visibility: visible !important;
    display: flex;
    height: 100%;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    box-sizing: border-box;
  }
  .mobile-sidebar {
    // visibility: visible !important;
    position: fixed;
    width: 0;
    height: 100%;
    background: white;

    transition: 0.1s ease-in-out;
    z-index: 1000;
    -webkit-box-shadow: 10px 10px 19px -5px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: 10px 10px 19px -5px rgba(0, 0, 0, 0.75);
    box-shadow: 10px 10px 19px -5px rgba(0, 0, 0, 0.75);
    box-sizing: border-box;

    ul {
      display: flex;
      flex-direction: column;
      list-style-type: none;
      padding: 0;

      a {
        text-decoration: none;
        color: black;
      }
      li {
        height: 70px;
        width: 100%;
        border-bottom: 1px solid lightgrey;
        font-weight: bold;
        font-size: 1.4em;
        display: flex;
        align-items: center;
        padding-left: 20px;
      }
    }
  }

  .open {
    width: 300px;
    * {
      visibility: visible !important;
    }
  }
}
</style>