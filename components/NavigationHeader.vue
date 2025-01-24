<template>
  <header>
    <div class="navbar">
      <div class="container">
        <div class="logo">
          <picture>
            <source
              type="image/webp"
              srcset="~/assets/imgs/logo-and-exclam.webp"
            />
            <img src="~/assets/imgs/logo-and-exclam.png" alt="" />
          </picture>
          <h1>農地違章工廠</h1>
        </div>

        <nav>
          <ul>
            <li
              v-for="item in navList"
              :key="item.id"
              @click="handleClick(item.id, item.evtAction)"
            >
              {{ item.text }}
            </li>
          </ul>
          <a
            href="https://bit.ly/3kESSsQ"
            target="_blank"
            rel="noopener"
            @click="$ga.event('navigator', 'go2reportheader', 'navigator')"
            >拍照回報</a
          >
          <a
            class="go2spotdiff"
            href="https://bit.ly/3vFXXaj"
            target="_blank"
            rel="noopener"
            @click="$ga.event('navigator', 'go2spotdiffheader', 'navigator')"
            >鍵盤參與</a
          >
        </nav>

        <div class="menu-icon" @click="toggleSidebar">
          <SvgClose v-if="shouldOpenSidebar" />
          <SvgHamberger v-else class="hamberger" />
        </div>
      </div>
    </div>

    <transition name="slide">
      <div v-if="shouldOpenSidebar" class="sidebar">
        <ul>
          <li
            v-for="item in navList"
            :key="item.id"
            @click="handleClick(item.id, item.evtAction)"
          >
            {{ item.text }}
          </li>
          <li>
            <a
              href="https://bit.ly/3kESSsQ"
              target="_blank"
              rel="noopener"
              @click="$ga.event('navigator', 'go2reportheader', 'navigator')"
              >拍照回報</a
            >
          </li>
          <li>
            <a
              class="go2spotdiff"
              href="https://bit.ly/3vFXXaj"
              target="_blank"
              rel="noopener"
              @click="$ga.event('navigator', 'go2spotdiffheader', 'navigator')"
              >鍵盤參與</a
            >
          </li>
        </ul>
      </div>
    </transition>
  </header>
</template>

<script>
import { ref } from '@vue/composition-api'
import SvgHamberger from '~/assets/imgs/hamberger.svg?inline'
import SvgClose from '~/assets/imgs/close-cross.svg?inline'

export default {
  name: 'NavigationHeader',

  components: {
    SvgHamberger,
    SvgClose,
  },

  setup(_, { root: { context: ctx } }) {
    const shouldOpenSidebar = ref(false)

    function toggleSidebar() {
      shouldOpenSidebar.value = !shouldOpenSidebar.value
    }
    function closeSidebar() {
      shouldOpenSidebar.value = false
    }

    function handleClick(id, evtAction) {
      scrollTo(id)
      closeSidebar()

      ctx.$ga.event('navigator', evtAction)
    }

    async function scrollTo(id) {
      const scrollIntoView = (await import('scroll-into-view')).default

      scrollIntoView(document.getElementById(id), {
        time: 300,
        align: {
          topOffset: 55,
        },
        ease: (t) => t * t * t,
      })
    }

    return {
      shouldOpenSidebar,
      toggleSidebar,

      navList: [
        {
          id: 'do-you-know',
          text: '你知道嗎？',
          evtAction: 'doyouknow',
        },
        {
          id: 'report',
          text: '回報系統',
          evtAction: 'report_system_intro',
        },
        {
          id: 'current-results',
          text: '目前成果',
          evtAction: 'current_results',
        },
        {
          id: 'faq',
          text: '常見問題',
          evtAction: 'Q&A',
        },
        {
          id: 'media',
          text: '新聞報導',
          evtAction: 'media',
        },
      ],
      handleClick,
    }
  },
}
</script>

<style lang="scss">
body {
  padding-top: 55px;
}
</style>

<style lang="scss" scoped>
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 55px;
  z-index: 99;
  color: #2b4754;
  @include media-breakpoint-up(lg) {
    height: 60px;
  }
}

li {
  cursor: pointer;
  user-select: none;
}
/* stylelint-disable no-descending-specificity */
a {
  border: 2px solid #697f01;
  letter-spacing: 0.7px;
  color: #697f01;
  font-weight: 700;
  transition: background-color 0.2s;
  &:hover {
    background-color: #eaf3bf;
  }
  & + a {
    margin-left: 17px;
  }
}
.go2spotdiff {
  color: #107393;
  border: 2px solid #107393;
  &:hover {
    background-color: #e5f3f3;
  }
}

.navbar {
  background-color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
  padding: 0 16px;
  height: 100%;

  ul {
    display: flex;
    font-size: 16px;
  }

  li {
    margin-right: 32px;
    &:last-child {
      margin-right: 17px;
    }
  }

  a {
    border-radius: 24px;
    font-size: 16px;
    padding: 4px 16px;
  }
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}

img {
  width: 53px;
  margin-right: 15px;
  @include media-breakpoint-up(lg) {
    width: 58px;
  }
}

h1 {
  font-size: 20px;
  letter-spacing: 1.86px;
  @include media-breakpoint-up(lg) {
    font-size: 23px;
  }
}

.logo {
  display: flex;
  align-items: center;
}

nav {
  display: none;
  @include media-breakpoint-up(lg) {
    display: flex;
    align-items: center;
  }
}

.menu-icon {
  cursor: pointer;
  @include media-breakpoint-up(lg) {
    display: none;
  }
}

svg {
  display: block;
}

.sidebar {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 55px;
  left: 0;
  padding: 32px;
  background-color: #fbfdf0;
  font-size: 30px;
  color: #457287;
  z-index: -1;

  li {
    margin-bottom: 28px;

    &:nth-child(5) {
      margin-bottom: 36px;
    }
  }
  a {
    display: block;
    width: 144px;
    border: 2px solid #697f01;
    box-sizing: border-box;
    border-radius: 35px;
    font-size: 19px;
    line-height: 28px;
    padding: 7px 19px;
    text-align: center;
  }
}

.slide {
  &-enter-active,
  &-leave-active {
    transition: transform 0.3s;
  }

  &-enter,
  &-leave-to {
    transform: translateX(-100%);
  }
}
</style>
