<template>
  <div>
    <div class="nav">
      <div class="project-name">DICTIONARY</div>
      <div class="nav-items">
        <ul>
          <router-link tag="li" activeClass="active" exact to="/"><a>Home</a></router-link>
          <router-link tag="li" activeClass="active" to="/about"><a>About</a></router-link>
          <a href="" tag="li" target="_blank"> <img src="../assets/github.svg" alt="" class="image"> </a>
        </ul>
      </div>
      <span tag="li" class="menu-icon" @click="showRightMenu">&#9776;</span>
    </div>
    <transition name="animate" mode="out-in">
      <div class="right-menu" ref="rightMenu">
        <div @click="hideRightMenu">
          <router-link activeClass="active" exact to="/"><a>Home</a></router-link>
        </div>
        <div @click="hideRightMenu">
          <router-link activeClass="active" to="/about"><a>About</a></router-link>
        </div>
        <div>
          <a href="" tag="li" target="_blank"> <img src="../assets/github.svg" alt="" class="image"> </a>
        </div>
      </div>
    </transition>

  </div>
</template>
<script>
export default {
  methods: {
    showRightMenu () {
      if (this.$refs.rightMenu.style.display === 'block') {
        this.$refs.rightMenu.style.display = 'none'
      } else {
        this.$refs.rightMenu.style.display = 'block'
      }
    },
    hideRightMenu () {
      this.$refs.rightMenu.style.display = 'none'
    }
  },
  mounted () {
    window.addEventListener('resize', () => {
      if (window.innerWidth >= 760) {
        this.$refs.rightMenu.style.display = 'none'
      }
    })
  }
}
</script>
<style scoped>
  .nav {
    background-color: #4655A0;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    color: #fff;
    padding-left: 1rem;
    font-size: 1.6rem;
  }
  ul {
    display: flex;
  }
  ul li {
    list-style-type: none;
    margin-right: 1rem;
  }
  ul li a {
    color: #fff;
    text-decoration: none;
  }
  .image {
    width: 20px;
    height: 17px;
    margin-right: 1rem;
    color: #fff;
  }
  .active {
    border-bottom: 2px solid #ccc;
  }
  .project-name {
    font-weight: bold;
    font-size: 2rem;
  }
  .menu-icon, .right-menu {
    display: none;
  }
  .right-menu {
    position: fixed;
    top: 100;
    right: 0;
    background-color: #fff;
    z-index: 1;
    width: 100%;
    font-size: 2rem;
    height: 100vh;
    text-align: center;
    box-shadow: 2px 2px 20px rgba(0,0,0,0.3);
    animation: animate 500ms ease-out forwards;
  }
  .right-menu a {
    text-decoration: none;
  }
  .right-menu div {
    margin: 20px 0px;
  }
  @media(max-width: 760px) {
    .menu-icon {
      display: block;
      cursor: pointer;
      margin: 1rem 1rem;
      font-size: 3rem;
      outline: none;
    }
    .nav-items {
      display: none;
    }
  }
  @keyframes animate {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
