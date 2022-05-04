<template>
  <footer>
    <picture>
      <source type="image/webp" srcset="~/assets/imgs/earth-and-g0v.webp" />
      <img src="~/assets/imgs/earth-and-g0v.png" alt="" />
    </picture>

    <div class="containr">
      <p class="contact">聯繫地球公民基金會</p>
      <p>
        Email:
        <a href="https://github.com/Disfactory" target="_blank" rel="noopener"
          >cet@cet-taiwan.org</a
        >
      </p>
      <p>電話：02-23920371</p>
      <p>
        網站：<a
          href="https://github.com/Disfactory"
          target="_blank"
          rel="noopener"
          >https://www.cet-taiwan.org</a
        >
      </p>
    </div>

    <p class="license">
      全站由使用者回報之資料及設計圖以CC
      BY姓名標示4.0釋出，標註「農地違章工廠回報系統貢獻者」，原始碼已MIT開放授權公開在<a
        href="https://github.com/Disfactory"
        target="_blank"
        rel="noopener"
        >GitHub</a
      >上。使用者回報資料未涉及個人資訊部分已整理成開放資料與<a
        href="https://api.disfactory.tw/redoc/"
        target="_blank"
        rel="noopener"
        >API</a
      >。<a class="contributor-list" @click.prevent="openModal">貢獻者名單</a>
    </p>
    <transition name="modal">
      <div v-if="showModal" class="modal-shadow" @click.self="closeModal">
        <div class="modal-body">
          <SvgClose class="modal-close" @click="closeModal" />
          <div class="modal-content">
            <div class="title">貢獻者</div>
            <div class="introduction">
              <p class="thanks">謝謝！</p>
              <div>
                <p>Disfactory.tw 為農地違章工廠的回報平台</p>
                <p>
                  project is run by volunteers in the g0v.tw civic hacker
                  network.
                </p>
                <p>
                  Don't ask why nobody is doing this. <br />Become that nobody.
                </p>
              </div>
            </div>

            <div class="list">
              <div class="group">
                <div class="group-name">前端</div>
                <div class="group-member">
                  <p>IU、yukai、yeefun、dotsea、Caleb</p>
                </div>
              </div>
              <div class="group">
                <div class="group-name">設計</div>
                <div class="group-member">
                  <p>SL、J、Tin、Lydia、Xinroo、RAY</p>
                </div>
              </div>
              <div class="group">
                <div class="group-name">後端</div>
                <div class="group-member">
                  <p>
                    cph、yellowsoar、swind、小白、YAlgorithm、sour、Jsaon、Toby、
                    Sonia、Andy、Hubert、Darren、Looofy、Simon、Aaron
                  </p>
                </div>
              </div>
              <div class="group">
                <div class="group-name">圖資/GIS</div>
                <div class="group-member">
                  <p>chewei、ronnywang、bdon、pm5、kiang、shupo</p>
                </div>
              </div>
              <div class="group">
                <div class="group-name">PM</div>
                <div class="group-member">
                  <p>ael</p>
                </div>
              </div>
              <div class="group">
                <div class="group-name">地球公民基金會</div>
                <div class="group-member">
                  <p>小海、deeper、小胖、沅諭、可飛、peii</p>
                </div>
              </div>
              <div class="group">
                <div class="group-name">社群協力</div>
                <div class="group-member">
                  <p>
                    ddio、chiahe、Joycelin、laiTzan、chelin、jenhaoyang、chihao、Angel、安東尼、Bryce、笑笑、積丹尼、誠夏、Stasia、慈忻、Kai、昱伶、Tai、Wuulong、Carmen、fly、土撥鼠、mhshih、JinWen、Johnson、John
                    Huang、zyan、tai、slayer、mg、robin、星穎、ichieh、isabel、Tiff、雅安、Jay
                    Lo、mcdlee、CRW、Guo-Jim
                  </p>
                </div>
              </div>
            </div>
            <p class="thanks">謝謝！</p>
          </div>
        </div>
      </div>
    </transition>
  </footer>
</template>

<script>
import SvgClose from '~/assets/imgs/close-cross.svg?inline'

export default {
  name: 'TheFooter',
  components: {
    SvgClose,
  },
  data() {
    return {
      showModal: false,
    }
  },

  methods: {
    //   when modal is opened, freeze scroll bar of the page
    openModal() {
      this.showModal = true
      document.documentElement.style.overflow = 'hidden'
    },
    //   when modal is closed, unfreeze scroll bar of the page
    closeModal() {
      this.showModal = false
      document.documentElement.style.overflow = 'auto'
    },
  },
}
</script>

<style lang="scss" scoped>
footer {
  font-size: 18px;
  padding: 40px 0;
  @include media-breakpoint-up(lg) {
    padding: 40px 0 48px 0;
  }
}

img {
  width: 160px;
  margin: 0 auto;
  margin-bottom: 12px;
}

a {
  color: inherit;
  text-decoration: underline;
}

.containr {
  border-top: 1px solid #d9e0a2;
  padding: 32px 32px 0 32px;
  max-width: 376px;
  margin: 0 auto;
  box-sizing: border-box;

  p + p {
    margin-top: 5px;
  }
}

.contact {
  font-weight: 700;
  margin-bottom: 8px;
}

.license {
  text-align: center;
  font-size: 15px;
  color: #a1a1a1;
  margin: 45px auto 0 auto;
  padding: 0 32px;
  max-width: 800px;
  .contributor-list {
    color: #5f5f5f;
  }
}
.modal-shadow {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 10;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  @include media-breakpoint-up(lg) {
    z-index: 1000;
  }
}
.modal-body {
  display: block;
  position: absolute;
  left: 50vw;
  top: 70px;
  transform: translate(-50%, 0%);
  border-radius: 10px;
  background-color: #fff;
  border: 1px solid #888;
  width: calc(100% - 30px);
  padding-top: 40px;
  padding-bottom: 20px;
  @include media-breakpoint-up(lg) {
    left: 50vw;
    top: 50vh;
    transform: translate(-50%, -50%);
    max-width: 776px;
  }
}
.modal-content {
  text-align: center;
  font-size: 16px;
  height: calc(100vh - 140px);
  overflow-y: scroll;
  padding-left: 16px;
  padding-right: 16px;
  @include media-breakpoint-up(lg) {
    max-height: 706px;
    padding-left: 70px;
    padding-right: 70px;
  }
  .title {
    font-size: 38px;
    line-height: 55px;
    padding-bottom: 37px;
  }
  .thanks {
    font-weight: 500;
    font-style: normal;
    font-size: 26px;
    line-height: 30px;
    color: #2b4754;
    @include media-breakpoint-up(lg) {
      display: none;
    }
  }
  .introduction {
    font-weight: 400;
    font-style: normal;
    margin: 0 auto;
    width: 100%;
    text-align: left;
    line-height: 1.25;
    padding-bottom: 14px;
    border-bottom: 1px solid #9d9d9d;
    p {
      margin: 0 0 16px 0;
    }
    .thanks {
      display: none;
    }
    @include media-breakpoint-up(lg) {
      display: flex;
      justify-content: space-between;
      padding-bottom: 4px;
      .thanks {
        display: block;
        min-width: 140px;
        text-align: left;
        margin-right: 20px;
      }
    }
  }
  .list {
    padding: 30px 0 14px 0;
    .group {
      padding-bottom: 21px;
      line-height: 1.5;
      font-style: normal;
      .group-name {
        color: #107393;
        font-weight: 500;
      }
      .group-member {
        font-weight: 400;
        overflow-wrap: break-word;
      }
      @include media-breakpoint-up(lg) {
        display: flex;
        justify-content: start;
        .group-name {
          min-width: 140px;
          text-align: left;
          margin-right: 20px;
        }
        .group-member {
          text-align: left;
        }
      }
    }
  }
}

.modal-close {
  position: absolute;
  right: 17px;
  top: 17px;
  rect {
    fill: #979797;
  }
  &:hover,
  &:focus {
    text-decoration: none;
    cursor: pointer;
    rect {
      fill: #5f5f5f;
    }
  }
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 1s;
}
.modal-enter,
.modal-leave-to {
  opacity: 0;
}
.modal-enter-to,
.modal-leave {
  opacity: 1;
}
</style>
