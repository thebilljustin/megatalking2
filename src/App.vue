<template>
  <div id="app">
    <v-app>
      <v-card
        tile
        height="75"
        width="100%"
        style="position: fixed; top: 0; z-index: 100"
        v-if="showNav"
      >
        <v-container class="d-flex flex-row">
          <v-card flat tile color="#00000000">
            <v-img
              @click="$router.push('/')"
              contain
              src="../src/assets/logo.jpg"
              width="100"
              class="subheading"
            ></v-img>
          </v-card>

          <v-card
            v-if="screenWidth >= 960"
            flat
            class="d-flex align-center mx-auto"
            color="#00000000"
            style="color: #a3a3a3"
          >
            <div
              class="mr-6 subheading"
              v-for="(route, i) in routes"
              :key="i"
              @click="$router.push(`/${route.link}`)"
            >
              {{ route.text }}
            </div>
          </v-card>
          <v-card
            v-if="screenWidth > 960"
            flat
            class="d-flex align-center mr-5"
            color="#00000000"
            style="color: #a3a3a3"
          >
            <div class="mr-8 subheading" @click="$router.push('/account')">
              회원정보
            </div>
            <div class="mr-6 subheading" @click="signInDialog = true">
              <a>로그인</a>
            </div>
          </v-card>

          <v-spacer v-if="screenWidth <= 960"></v-spacer>

          <v-menu
            v-if="screenWidth <= 960"
            close-on-click
            min-width="100%"
            nudge-bottom="12"
            offset-y
            bottom
            class="mt-10 ml-auto"
            transition="slide-y-transition"
            tile
          >
            <template v-slot:activator="{ on: menu }">
              <v-icon v-on="menu" x-large>menu</v-icon>
            </template>
            <v-card
              style="color: #a3a3a3"
              minz-width="100%"
              color="#fafafa"
              tile
              flat
            >
              <v-list>
                <v-list-item
                  v-for="(route, i) in routes"
                  :key="i"
                  @click="$router.push(`/${route.link}`)"
                  >{{ route.text }}</v-list-item
                >
              </v-list>
            </v-card>
          </v-menu>
        </v-container>
      </v-card>

      <v-img
        :src="currentImage"
        width="showNav"
        class="text-center"
        v-if="showNav"
      >
        <router-view></router-view>

        <v-card max-width="1000" class="mx-auto mt-10" color="#00000000" flat>
          <v-container>
            <v-row no-gutters class="d-flex flex-column-reverse flex-md-row">
              <v-col cols="12" md="3">
                <v-container>
                  <v-row>
                    <div class="mb-4">고객센터 1688-5705</div>
                    <div class="caption text--secondary">
                      (평일 오전 9시~18시)
                    </div>
                  </v-row>
                  <v-row style="margin-top: 150px">
                    <v-card color="#00000000" flat>
                      <v-img
                        @click="$router.push('/')"
                        contain
                        src="../src/assets/mega_blue.png"
                        width="150"
                        class="subheading"
                      ></v-img>
                    </v-card>
                  </v-row>
                </v-container>
              </v-col>
              <v-col cols="12" md="5">
                <v-container>
                  <v-row>
                    <div class="mb-4">계좌번호 안내</div>
                  </v-row>
                  <v-row>
                    <div style="color: #cb5413" class="caption">
                      예금주 (주)유에듀케이션
                    </div>
                  </v-row>
                  <v-row class="mt-5">
                    <div class="caption text--secondary">
                      국민은행 466490-60-194511
                    </div>
                  </v-row>
                  <v-row>
                    <div class="caption text--secondary">
                      우리은행 605-747180-18892
                    </div>
                  </v-row>
                  <v-row>
                    <div class="caption text--secondary">
                      신한은행 562-01572-559672
                    </div>
                  </v-row>
                  <v-row>
                    <div class="caption text--secondary">
                      씨티은행 750-10229-91401
                    </div>
                  </v-row>
                  <v-row>
                    <div class="caption text--secondary">
                      농협 790007-52-578681
                    </div>
                  </v-row>
                  <v-row class="caption mt-10 text--secondary">
                    <div class="mr-3">(주)유에듀케이션</div>
                    <div class="mr-3">대표 정원석</div>
                    <div>사업자등록번호 124-87-33297</div>
                    <div>주소 경기 수원시 팔달구 인계동 1135-6 4층</div>
                  </v-row>
                </v-container>
              </v-col>
              <v-col>
                <v-container class="text--secondary">
                  <v-row>
                    <div style="letter-spacing: 5px">FOLLOW US</div>
                  </v-row>
                  <v-row>
                    <v-card class="d-flex flex-row mt-5" color="#00000000" flat>
                      <a
                        href="https://www.facebook.com/megatalking"
                        target="_blank"
                      >
                        <v-img
                          src="../src/assets/fa.png"
                          width="50"
                          class="mr-5"
                        ></v-img>
                      </a>
                      <a
                        href="https://www.instagram.com/megatalking_english/"
                        target="_blank"
                      >
                        <v-img
                          src="../src/assets/inst.png"
                          width="50"
                          class="mr-5"
                        ></v-img>
                      </a>
                    </v-card>
                  </v-row>
                </v-container>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-img>

      <router-view v-else></router-view>

      <v-dialog
        v-model="signInDialog"
        max-width="1000"
        style="
          overflow-x: hidden;
          lborder-radius: 25px 25px 25px 25px !important;
        "
      >
        <v-card flat class="rounded-xl" max-width="1000">
          <v-card flat color="#8aace9" class="rounded-xl">
            <v-container class="py-0">
              <v-row>
                <v-col cols="6" class="white--text">
                  <span class="ml-5 h5 nanum">회원 로그인</span>
                </v-col>
                <v-col cols="6" class="d-flex align-center white--text">
                  <span class="ml-5 h5 nanum">회원가입</span>
                  <v-spacer></v-spacer>
                  <span class="mr-5">
                    <v-icon color="white" @click="signInDialog = false">
                      close
                    </v-icon>
                  </span>
                </v-col>
              </v-row>
            </v-container>
            <v-card flat class="pa-5">
              <v-container>
                <v-row>
                  <v-col cols="5" class="mx-auto">
                    <v-row>
                      <v-col>
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="아이디(이메일)"
                        ></v-text-field>
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="비밀번호"
                        ></v-text-field>
                        <v-checkbox label="로그인 상태 유지"></v-checkbox>
                        <v-btn
                          style="
                            background-image: linear-gradient(
                              to right,
                              #add5f5,
                              #9ebbef
                            );
                          "
                          block
                          depressed
                          class="white--text h5 nanum rounded-xl"
                          large
                          >로그인</v-btn
                        >
                      </v-col>
                    </v-row>
                  </v-col>
                  <v-divider vertical></v-divider>
                  <v-col cols="5" class="mx-auto">
                    <v-row>
                      <v-col cols="12" md="6" class="py-0">
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="이름 "
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" md="6" class="py-0">
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="연락처"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" class="py-0">
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="이메일"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" md="6" class="py-0">
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="비밀번호 "
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" md="6" class="py-0">
                        <v-text-field
                          dense
                          outlined
                          class="rounded-xl"
                          label="비밀번호 확인"
                        ></v-text-field>
                      </v-col>
                      <v-checkbox
                        label="아래 약관에 모두 동의합니다.s"
                      ></v-checkbox>
                      <v-checkbox
                        label="만 14세 이상이며, 전화영어 이용약관, 개인정보 수집 및 이용에 동의"
                      ></v-checkbox>
                      <v-checkbox
                        class="mt-0"
                        label="할인/이벤트 안내 동의(선택)"
                      ></v-checkbox>
                      <v-btn
                        style="
                          background-image: linear-gradient(
                            to right,
                            #fc686f,
                            #ff934d
                          );
                        "
                        block
                        depressed
                        class="white--text h5 nanum rounded-xl"
                        large
                        >신규 회원가입</v-btn
                      >
                    </v-row>
                  </v-col>
                </v-row>
              </v-container>
            </v-card>
          </v-card>
        </v-card>
      </v-dialog>
    </v-app>
  </div>
</template>

<style scoped>
.subheading {
  cursor: pointer;
}
</style>

<script>
export default {
  data() {
    return {
      showNav: true,
      currentRoute: "main",
      signInDialog: false,

      routes: [
        {
          text: "커리큘럼",
          link: "curriculum",
        },
        {
          text: "레벨테스트",
          link: "level-test",
        },
        {
          text: "수강신청",
          link: "enrollment",
        },
        {
          text: "마이페이지",
          link: "mypage",
        },
        {
          text: "수강후기",
          link: "board",
        },
        {
          text: "이벤트",
          link: "event",
        },
      ],

      images: {
        main: require("../src/assets/main.jpg"),
        curriculum: require("../src/assets/curriculum.jpg"),
        leveltest: require("../src/assets/leveltest.jpg"),
        enrollment: require("../src/assets/enrollment.jpg"),
        mypage: require("../src/assets/bg_mega_review.png"),
        board: require("../src/assets/bg_mega_review.png"),
        event: require("../src/assets/bg_mega_event.png"),
      },
      currentImage: "",
      screenWidth: "",
      isMobile: false,
    };
  },

  created() {
    window.addEventListener("resize", this.onWindowResize);
  },
  destroyed() {
    window.removeEventListener("resize", this.onWindowResize);
  },

  mounted() {
    if (this.$route.path == "/material") {
      this.showNav = false;
    } else {
      this.showNav = true;
      this.loadBg();
    }

    this.screenWidth = screen.width;
    this.isMobile = this.screenWidth <= 960 ? true : false;
  },

  watch: {
    $route: function () {
      if (this.$route.path == "/material") {
        this.showNav = false;
      } else {
        this.showNav = true;
        this.loadBg();
      }
    },
  },

  methods: {
    loadBg() {
      if (this.$route.path == "/") {
        this.currentImage = this.images.main;
      } else if (this.$route.path == "/level-test") {
        this.currentImage = this.images.leveltest;
      } else {
        this.currentRoute = this.$route.path.slice(1, this.$route.path.length);
        console.log(this.currentRoute);
        this.currentImage = this.images[this.currentRoute];
      }
    },

    onWindowResize() {
      this.screenWidth = screen.width;
      this.isMobile = this.screenWidth <= 960 ? true : false;
    },
  },
};
</script>

<style>
#app {
  /* font-family: "Nanum Gothic", sans-serif; */
  font-family: "NanumSquare", sans-serif;
}
/* #app {
  font-family: "NanumSquare";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
} */

.text-purple {
  color: #5a55a1;
}

.text-dark-purple {
  color: #475ba4;
}

.icon-large {
  font-size: 48px;
}

.shadow {
  box-shadow: 0 4px 5px -2px rgba(179, 203, 240, 0.2),
    0 7px 10px 1px rgba(0, 0, 0, -0.86), 0 2px 16px 1px rgba(0, 0, 0, 0.12) !important;
}

.h1 {
  font-weight: 300;
  font-size: 6rem;
  letter-spacing: -0.09375rem;
}
.h2 {
  font-weight: 300;
  font-size: 3.75rem;
  letter-spacing: -0.03125rem;
}
.h3 {
  font-family: "GmarketSansGmarketSansBoldLight", sans-serif;
  font-weight: 400;
  font-size: 3rem;
  letter-spacing: normal;
}
.h4 {
  font-family: "GmarketSansBold", sans-serif;
  font-weight: 400;
  font-size: 2.125rem;
  letter-spacing: -0.015625remm;
}
.h5 {
  font-family: "GmarketSansBold", sans-serif;
  font-weight: 400;
  font-size: 1.5rem;
  letter-spacing: normal;
  line-break: strict;
  word-break: keep-all;
}
.h6 {
  font-weight: 500;
  font-size: 1.25rem;
  letter-spacing: 0.009375rem;
}

.subtitle-text-1 {
  font-weight: 400;
  font-size: 1rem;
  letter-spacing: 0.009375rem;
}

.regular {
  font-weight: 400 !important;
}

.v-application .caption {
  font-family: unset;
}

.caption-text {
  font-family: "NanumSquare", sans-serif;
  font-size: 0.8rem;
  font-weight: 400;
  letter-spacing: 0.025rem;
}

.nanum {
  font-family: "NanumSquare", sans-serif !important;
}

.gmarket {
  font-family: "GmarketSansBold", sans-serif !important;
}

.korean-text {
  word-break: keep-all;
  line-break: strict;
}

@font-face {
  font-family: "GmarketSansBold";
  src: url("https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansBold.woff")
    format("woff");
  font-weight: normal;
  font-style: normal;
}

/* @font-face {
  font-family: "NanumSquareB";
  font-style: normal;
  src: url("https://cdn.jsdelivr.net/npm/typeface-nanum-square@1.1.0/NanumSquareB.woff")
      format("woff"),
    url("https://cdn.jsdelivr.net/npm/typeface-nanum-square@1.1.0/NanumSquareB.woff2")
      format("woff2");
}

@font-face {
  font-family: "NanumSquare";
  font-style: normal;
  src: url("https://cdn.jsdelivr.net/npm/@kfonts/nanum-square@0.1.0/NanumSquareRegular.woff")
      format("woff"),
    url("https://cdn.jsdelivr.net/npm/@kfonts/nanum-square@0.1.0/NanumSquareRegular.woff2")
      format("woff2");
} */
</style>

