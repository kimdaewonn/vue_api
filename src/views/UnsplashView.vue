<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="reperence api" />
    <section class="cont__refer">
      <div class="container">
        <div class="unsplash__inner">
          <div class="unsplash__slider">
            <div class="container">
              <h2>Unsplash Random</h2>
              <swiper
                :autoplay="{
                  delay: 2500,
                  disableOnInteraction: false,
                }"
                :slidesPerView="3"
                :spaceBetween="30"
                :freeMode="true"
                :pagination="{
                  clickable: true,
                }"
                :modules="modules"
                class="mySwiper"
              >
                <swiper-slide v-for="random in randoms" :key="random.id">
                  <li>
                    <a :href="`https://unsplash.com/photos/${random.id}`">
                      <img
                        :src="`${random.urls.regular}`"
                        :alt="`${random.urls.alt_description}`"
                      />
                    </a>
                  </li>
                </swiper-slide>
              </swiper>
            </div>
          </div>
          <div className="unsplash__search">
            <div className="container">
              <h2 class="blind">검색하기</h2>
              <form @submit.prevent="SearchSplashes()">
                <input
                  type="search"
                  id="search"
                  placeholder="검색하세요!"
                  v-model="search"
                />
                <button class="unsplash_search_btn" type="submit">검색</button>
              </form>
            </div>
          </div>
          <div className="unsplash__btn">
            <div className="container">
              <button
                type="submit"
                v-on:click="SearchSplashes(title.text)"
                v-for="title in titles"
                v-bind:key="title.text"
              >
                {{ title.text }}
              </button>
            </div>
          </div>
          <div class="unsplash__images">
            <ul>
              <li v-for="splash in splashes" :key="splash.id">
                <a :href="`https://unsplash.com/photos/${splash.id}`">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

import { Swiper, SwiperSlide } from "swiper/vue";

import "swiper/css";

import "swiper/css/free-mode";
import "swiper/css/pagination";
import { FreeMode, Pagination, Autoplay } from "swiper";

export default {
  components: {
    HeaderCont,
    TitleCont,
    FooterCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const randoms = ref([]);
    const splashes = ref([]);
    const search = ref("landscape");

    const SearchSplashes = (e) => {
      fetch(
        `https://api.unsplash.com/search/photos?client_id=MQTjZPliVmEwJE8bRXeYPG83q1gT78-3AjOvYV4HNQk&query=${search.value}`
      )
        .then((response) => response.json())
        .then((result) => {
          splashes.value = result.results;
          search.value = "";
          search.value = e;
        })

        .catch((error) => console.log("error", error));
    };
    SearchSplashes();

    const RandomSplashes = () => {
      fetch(
        "https://api.unsplash.com/photos/random?client_id=MQTjZPliVmEwJE8bRXeYPG83q1gT78-3AjOvYV4HNQk&count=10"
      )
        .then((response) => response.json())
        .then((result) => (randoms.value = result))
        .catch((error) => console.log("error", error));
    };
    RandomSplashes();

    return {
      splashes,
      search,
      randoms,
      SearchSplashes,
      RandomSplashes,
      modules: [FreeMode, Pagination, Autoplay],
    };
  },

  data: function () {
    return {
      titles: [
        { text: "spring" },
        { text: "summer" },
        { text: "fall" },
        { text: "winter" },
        { text: "food" },
        { text: "space" },
        { text: "pretty" },
      ],
    };
  },
};
</script>

<style lang="scss">
.unsplash__images {
  ul {
    column-count: 4;
    column-gap: 20px;
    width: 100%;

    li {
      margin-bottom: 20px;

      img {
        border-radius: 5px;
      }
    }
  }
}

.unsplash__btn {
  button {
    margin-right: 5px;
    margin-top: 30px;
    padding: 10px 20px;
    margin-bottom: 10px;
    border-radius: 10px;
    background: #000;
    color: #fff;
    cursor: pointer;

    &:hover {
      background: #fff;
      color: #000;
    }
  }
}

.unsplash__inner {
  h2 {
    color: #000;
    font-size: 50px;
    margin-bottom: 30px;
    text-align: center;
  }
  .swiper-wrapper {
    height: 250px;
  }
  ul {
    column-count: 4;
    column-gap: 20px;
    width: 100%;
    li {
      margin-bottom: 20px;

      img {
        border-radius: 5px;
      }
    }
  }
}
.container {
  position: relative;
  input {
    margin-top: 30px;
    background: rgb(71, 69, 69);
    border: 2px solid var(--white);
    border-radius: 30px;
    color: #fff;
    width: 100%;
    padding: 10px 40px;
    font-family: var(--font-kor2);
  }
  .unsplash_search_btn {
    position: absolute;
    right: 0px;
    top: 30px;
    width: 70px;
    height: 50px;
    border-radius: 10px !important;
    border: 0;
    font-family: var(--font-kor2);
    cursor: pointer;
    z-index: 1000;
    white-space: nowrap;
  }
  ::placeholder {
    color: #fff;
  }
}
</style>
