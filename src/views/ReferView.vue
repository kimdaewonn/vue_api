<template>
  <div>
    <HeaderCont />
    <TitleCont name1="reference" name2="reference api" />

    <section className="cont__refer">
      <div className="container">
        <div className="refer__inner">
          <h2>CSS</h2>
          <ul className="refer__list">
            <li v-for="refer in refers" :key="refer.title">
              <a href="/">
                <span class="num">{{ refer.num }}</span>
                <span class="title">{{ refer.title }}</span>
                <span class="desc">{{ refer.desc }}</span>
                <span class="descStar">{{ refer.descStar }}</span>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </section>

    <FooterCont />
    <ContactCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const refers = ref([]);

    const references = () => {
      fetch(
        "https://raw.githubusercontent.com/kimdaewonn/react_api/main/src/utils/cssRefer.json"
      )
        .then((response) => response.json())
        // .then((result) => console.log(result.cssRefer))
        .then((result) => (refers.value = result.cssRefer))
        .catch((error) => console.log("error", error));
    };
    references();

    return {
      refers,
      references,
    };
  },
};
</script>
<style lang="scss">
.refer__inner {
  padding-bottom: 200px;

  h2 {
    font-size: 30px;
    color: var(--black);
  }
}

.refer__list {
  border: 1px solid var(--bg-dark-border);
  border-top-width: 2px;

  li {
    border-bottom: 1px solid var(--bg-dark-border);
    a {
      display: flex;
      align-items: center;
      width: 100%;
      color: var(--black);
      font-family: var(--font-kor2);

      span {
        display: inline-block;
        padding: 15px 20px;
      }

      .num {
        flex: 1 1 5%;
        text-align: center;
        border-right: 1px solid var(--bg-dark-border);
      }
      .title {
        flex: 1 1 20%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .desc {
        flex: 1 1 65%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .descStar {
        flex: 1 1 10%;
        text-align: center;
      }
    }
  }
}
</style>
