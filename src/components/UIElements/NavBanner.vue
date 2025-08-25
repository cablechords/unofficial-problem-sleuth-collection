<template>
  <nav class="navBanner" :class="{customNavBanner: useCustomStyles, pixelated: $localData.settings.pixelScaling}">
    <div class="navList">
      <img src="assets://archive/collection/mspa_menu.gif" usemap="#menumap">
      <a href="/" style="text-decoration: none;"><img src="assets://archive/collection/logo.gif"></a>
      <img src="assets://archive/collection/mspa_menu2.gif">
      <map name="menumap" id="menumap">
        <area shape="poly" coords="4,21,23,51,64,34,47,3" href="/map" alt="Map">
        <area shape="poly" coords="19,70,19,79,55,99,77,85,77,78,55,63,71,50,76,34,58,42,46,60,39,56" href="/help" alt="Save">
        <area shape="poly" coords="81,21,72,22,73,7,122,1,135,49,145,49,139,57,91,67" href="/log" alt="Log">
        <area shape="poly" coords="87,77,93,95,122,96,122,99,130,98,131,94,155,88,149,71,133,65,104,69" href="/help" alt="Load">
        <area shape="poly" coords="145,26,156,4,200,21,187,43,165,41,159,59,150,57,158,36" href="/search" alt="Search">
        <area shape="poly" coords="180,96,160,87,159,66,180,57,200,68,201,85" href="/help" alt="Faqs">
      </map>
    
    </div>
  </nav>
</template>

<script>

import Media from '@/components/UIElements/MediaEmbed.vue'

export default {
  name: 'navBanner',
  components: {
  },
  props: [
    'useCustomStyles'
  ],
  data: function() {
    return {
      // MS PAINT ADVENTURES
      // ARCHIVE | NEW READER?
      // MAP | LOG | SEARCH
      // SHOP | MUSIC
      // FORUMS | SECRETS | CREDITS
      urls: [
        [
          "/"
        ],
        [
          "/help"
        ],
        [
          "/map",
          "/log",
          "/search"
        ],
        [
          "/news",
        ],
        [
          "/evenmore",
          "/settings",
          "/credits"
        ]
      ],
      labels: {
        // list<theme => list<href => label>>
        // default theme in settings is the empty string
        mspa: {
          "https://www.homestuck.com": "HOMESTUCK.COM",
          "/": "PROBLEM SLEUTH COLLECTION",

          "toggleJumpBox": "JUMP",
          "/help": "HELP",

          "/map": "MAP",
          "/log": "LOG",
          "/search": "SEARCH",

          "/news": "NEWS",
          "toggleBookmarks": "SAVE/LOAD",

          "/evenmore": "MORE",
          "/settings": "SETTINGS",
          "/credits": "CREDITS"
        }
      }
    }
  },
  methods: {
    toggleBookmarks(){
      this.tabComponent.$refs.bookmarks.toggle()
    },
    toggleJumpBox(){
      this.$root.app.openJumpbox()
    },
    getLabel(href){
      // Tries to get a themed label, otherwise just prints the URL
      return this.labelDict[href] || href
    }
  },
  computed: {
    tabComponent() {
      return this.$root.app.activeTabComponent
    },
    labelDict() {
      return this.labels[this.$root.tabTheme.rendered] || this.labels['mspa']
    }
  }
}
</script>

<style lang="scss" scoped>
  .customNavBanner {
    background: var(--nav-bg);

    .navList {
      .candyCorn {
        content: var(--nav-candyCornContent);
      }
      ul li:before {
        color: var(--nav-divider);
      }
    }
    
    .nav1 a, .nav1 a:active {
      color: var(--nav-link, #ffffff);
    }
    .nav2 a, .nav2 a:active {
      color: var(--nav-link, #29ff4a);
    }
    .nav3 a, .nav3 a:active {
      color: var(--nav-link, #39d5f6);
    }
    .nav4 a, .nav4 a:active {
      color: var(--nav-link, #f7f72a);
    }
    .nav5 a, .nav5 a:active {
      color: var(--nav-link, #ffb529);
    }
  }

  a {
    text-decoration: underline;
    &:hover {
      cursor: pointer;
    }
  }

  .nav1 a, .nav1 a:active {
    color: #ffffff
  }
  .nav2 a, .nav2 a:active {
    color: #29ff4a;
  }
  .nav3 a, .nav3 a:active {
    color: #39d5f6;
  }
  .nav4 a, .nav4 a:active {
    color: #f7f72a;
  }
  .nav5 a, .nav5 a:active {
    color: #ffb529;
  }
  nav {
    background: #5a5a5a;
    width: 800px;
    max-width: 100vw;
    height: 117px;
    display: flex;
    align-content: center;
    justify-content: center;
    position: relative;

    .navList {
      display: flex;
      align-items: center;
      justify-content: center;
      .candyCorn {
        margin: 0 9px;
        content: url(assets://images/candycorn.gif);
      }
      ul {
        height: 17px;
        max-height: 17px;
        display: inline-flex;
        align-content: center;

        list-style: none;
        font-size: 10px;
        line-height: 10px;
        font-family: Arial, Helvetica, sans-serif;
        font-weight: 700;
        li {
          display: inline-flex;
          align-content: center;
          align-items: center;
          justify-content: center;
        }
        li + li:before {
          content: " | ";
          color: #FFFFFF;
          display: inline-block;
          margin: 0 0.3em
        }
      }
    }
  }
</style>
