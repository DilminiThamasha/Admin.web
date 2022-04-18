<template>
  <div
    class="sidebar"
    :class="isOpened ? 'open' : ''"
    :style="cssVars"
  >
    <div
      class="logo-details"
      style="margin: 6px 14px 0 14px;"
    >
      <div class="logo">
      <img src="../assets/logo.png" alt="Vue">
    </div>
      <div class="logo_name">
        <p>YourWay</p>
      </div>
      <i
        class="bx"
        :class="isOpened ? 'bx-menu-alt-right' : 'bx-menu'"
        id="btn"
        @click="isOpened = !isOpened"
      />
    </div>

    <div style="display:flex ;
                flex-direction:column;
                justify-content: space-between;
                flex-grow: 1;
                max-height: calc(100% - 60px); ">
      <div
        id="my-scroll"
        style="margin: 0px 0px 0 -10px;"
      >
        <ul
          class="nav-list"
          style="overflow:hidden;"
        >
         <span
            v-for="(menuItem, index) in menuItems"
            :key="index"
          >
            <li>
              <a :href="menuItem.link">
                <i
                  class="bx"
                  :class="menuItem.icon || 'bx-square-rounded'"
                />
                <span class="links_name">{{ menuItem.name }}</span>
              </a>
              <span class="tooltip">{{ menuItem.tooltip || menuItem.name }}</span>
            </li>
          </span>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    isMenuOpen: {
      type: Boolean,
      default: true
    },
    menuIcon: {
      type: String,
      default: 'bxl-c-plus-plus'
    },
    isPaddingLeft: {
      type: Boolean,
      default: true
    },
    menuOpenedPaddingLeftBody: {
      type: String,
      default: '250px'
    },
    menuClosedPaddingLeftBody: {
      type: String,
      default: '78px'
    },

    //! Menu items
    menuItems: {
      type: Array,
      default: () => [
        {
          link: '#',
          name: 'Dashboard',
          tooltip: 'Dashboard',
          icon: 'bx-grid-alt'
        },
        {
          link: '#',
          name: 'Buses',
          tooltip: 'Bus',
          icon: 'bx-bus'
        },
        {
          link: '#',
          name: 'Users',
          tooltip: 'User',
          icon: 'bx-group'
        },
        {
          link: '#',
          name: 'Track',
          tooltip: 'Track',
          icon: 'bx-map'
        },
        {
          link: '#',
          name: 'User Complaints',
          tooltip: 'User Complaints',
          icon: 'bx-chat'
        },
        {
          link: '#',
          name: 'Setting',
          tooltip: 'Setting',
          icon: 'bx-cog'
        }
      ]
    },

    //! Styles
    bgColor: {
      type: String,
      default: '#FFFFFF'
    },
    homeSectionColor: {
      type: String,
      default: '#371e69'
    },
    logoTitleColor: {
      type: String,
      default: '#0c0d0d'
    },
    iconsColor: {
      type: String,
      default: '#0c0d0d'
    },
    itemsTooltipColor: {
      type: String,
      default: '#e4e9f7'
    },
    menuItemsHoverColor: {
      type: String,
      default: '#4941f0'
    },
    menuItemsTextColor: {
      type: String,
      default: '#0c0d0d'
    },
    menuFooterTextColor: {
      type: String,
      default: '#fff'
    }
  },
  data () {
    return {
      isOpened: false
    }
  },
  mounted () {
    this.isOpened = this.isMenuOpen
  },
  computed: {
    cssVars () {
      return {
      // '--padding-left-body': this.isOpened ? this.menuOpenedPaddingLeftBody : this.menuClosedPaddingLeftBody,
        '--bg-color': this.bgColor,
        '--secondary-color': this.secondaryColor,
        '--home-section-color': this.homeSectionColor,
        '--logo-title-color': this.logoTitleColor,
        '--icons-color': this.iconsColor,
        '--items-tooltip-color': this.itemsTooltipColor,
        '--serach-input-text-color': this.searchInputTextColor,
        '--menu-items-hover-color': this.menuItemsHoverColor,
        '--menu-items-text-color': this.menuItemsTextColor,
        '--menu-footer-text-color': this.menuFooterTextColor
      }
    }
  },
  watch: {
    isOpened () {
      window.document.body.style.paddingLeft = this.isOpened && this.isPaddingLeft ? this.menuOpenedPaddingLeftBody : this.menuClosedPaddingLeftBody
    }
  }
}
</script>

<style>
  /* Google Font Link */
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap');
  @import url('https://unpkg.com/boxicons@2.0.7/css/boxicons.min.css');
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
  }
  body {
    transition: all 0.5s ease;
  }
  .logo {
    max-width: 30px;
    max-height: 50px;
    margin: 10px 0 10px;
    object-fit:fill;
  }
  .menuItem.icon{
      max-height: 20px;
      max-width: 10px;
      object-fit: contain;

  }
  .sidebar {
    position: relative;
    display: flex;
    flex-direction: column;
    position: fixed;
    left: 0;
    top: 0;
    height: 100%;
    min-height: min-content;
    /* overflow-y: auto; */
    width: 78px;
    background: var(--bg-color);
    /* padding: 6px 14px 0 14px; */
    z-index: 99;
    transition: all 0.5s ease;
  }
  .sidebar.open {
    width: 300px;
  }
  .sidebar .logo-details {
    height: 100px;
    display: flex;
    align-items: center;
    position: relative;
  }
  .sidebar .logo-details .icon {
    opacity: 0;
    transition: all 0.5s ease;
    align-items: center;
  }
  .sidebar .logo-details .logo_name {
    color: var(--logo-title-color);
    font-size: 35px;
    font-weight: 600;
    opacity: 0;
    transition: all 0.5s ease;
    margin-left: 25px;
    margin-top: 10px;
  }
  .sidebar.open .logo-details .icon,
  .sidebar.open .logo-details .logo_name {
    opacity: 5;
  }
  .sidebar .logo-details #btn {
    position: absolute;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    font-size: 20px;
    transition: all 0.4s ease;
    font-size: 30px;
    text-align: center;
    cursor: pointer;
    transition: all 0.5s ease;
  }
  .sidebar.open .logo-details #btn {
    text-align: right;
  }
  .sidebar i {
    color: var(--icons-color);
    height: 60px;
    min-width: 50px;
    font-size: 28px;
    text-align: center;
    line-height: 60px;
  }
  .sidebar .nav-list {
    margin-top: 20px;
    margin-bottom: 60px;
    height: 100%;
    min-height: min-content;
  }
  .sidebar li {
    position: relative;
    margin: 8px 0;
    list-style: none;
  }
  .sidebar li .tooltip {
    position: absolute;
    top: -20px;
    left: calc(100% + 15px);
    z-index: 3;
    background: transparent;
    box-shadow: 0 5px 10px rgba(237, 240, 235, 0.616);
    padding: 6px 12px;
    border-radius: 4px;
    font-size: 15px;
    font-weight: 400;
    opacity: 0;
    white-space: nowrap;
    pointer-events: none;
    transition: 0s;
  }
  .sidebar li:hover .tooltip {
    opacity: 1;
    pointer-events: auto;
    transition: all 0.4s ease;
    top: 50%;
    transform: translateY(-50%);
  }
  .sidebar.open li .tooltip {
    display: none;
  }
  .sidebar input {
    font-size: 15px;
    color: var(--serach-input-text-color);
    font-weight: 400;
    outline: none;
    height: 50px;
    width: 100%;
    width: 50px;
    border: none;
    border-radius: 12px;
    transition: all 0.5s ease;
    background: var(--secondary-color);
  }
  .sidebar.open input {
    padding: 0 20px 0 50px;
    width: 100%;
  }
  .sidebar li a {
    display: flex;
    height: 100%;
    width: 100%;
    border-radius: 12px;
    align-items: center;
    text-decoration: none;
    transition: all 0.4s ease;
    background: var(--bg-color);
  }
  .sidebar li a:hover {
    background: var(--menu-items-hover-color);
  }
  .sidebar li a .links_name {
    color: var(--menu-items-text-color);
    font-size: 15px;
    font-weight: 400;
    white-space: nowrap;
    opacity: 0;
    pointer-events: none;
    transition: 0.4s;
  }
  .sidebar.open li a .links_name {
    opacity: 1;
    pointer-events: auto;
  }
  .sidebar li a:hover .links_name,
  .sidebar li a:hover i {
    transition: all 0.5s ease;
    color: var(--bg-color);
  }
  .sidebar li i {
    height: 50px;
    line-height: 50px;
    font-size: 18px;
    border-radius: 12px;
  }
  .sidebar div.profile {
    position: relative;
    height: 60px;
    width: 78px;
    /* left: 0;
    bottom: 0; */
    padding: 10px 14px;
    background: var(--secondary-color);
    transition: all 0.5s ease;
    overflow: hidden;
  }
  .sidebar.open div.profile {
    width: 250px;
  }
  .sidebar div .profile-details {
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
  }
  .sidebar div img {
    height: 45px;
    width: 45px;
    object-fit: cover;
    border-radius: 6px;
    margin-right: 10px;
  }
  .sidebar div.profile .name,
  .sidebar div.profile .job {
    font-size: 15px;
    font-weight: 400;
    color: var(--menu-footer-text-color);
    white-space: nowrap;
  }
  .sidebar div.profile .job {
    font-size: 12px;
  }
  .sidebar .profile #log_out {
    position: absolute;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    background: var(--secondary-color);
    width: 100%;
    height: 60px;
    line-height: 60px;
    border-radius: 0px;
    transition: all 0.5s ease;
  }
  .sidebar.open .profile #log_out {
    width: 50px;
    background: var(--secondary-color);
    opacity: 0;
  }
  .sidebar.open .profile:hover #log_out {
    opacity: 1;
  }
  .sidebar.open .profile #log_out:hover {
    opacity: 1;
    color: red;
  }
  .sidebar .profile #log_out:hover {
    color: red;
  }
  .home-section {
    position: relative;
    background: var(--home-section-color);
    min-height: 100vh;
    top: 0;
    left: 78px;
    width: calc(100% - 78px);
    transition: all 0.5s ease;
    z-index: 2;
  }
  .sidebar.open ~ .home-section {
    left: 250px;
    width: calc(100% - 250px);
  }
  .home-section .text {
    display: inline-block;
    color: var(--bg-color);
    font-size: 25px;
    font-weight: 500;
    margin: 18px;
  }
  .my-scroll-active {
    overflow-y: auto;
  }
  #my-scroll {
    overflow-y: auto;
    height: calc(100% - 60px);
  }
  #my-scroll::-webkit-scrollbar{
    display:none;
    /* background-color: rgba(255, 255, 255, 0.2);
    width: 10px;
    border-radius:5px  */
  }
  /* #my-scroll::-webkit-scrollbar-thumb{
    background-color: red;
    border-radius:5px
  }
  #my-scroll::-webkit-scrollbar-button:vertical:start:decrement{
    display:none;
  }
  #my-scroll::-webkit-scrollbar-button:vertical:end:increment{
    display:none;
  } */
  @media (max-width: 420px) {
    .sidebar li .tooltip {
      display: none;
    }
}
</style>
