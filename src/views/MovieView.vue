<template>
  <div>
    <HeaderCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
  },
};
</script>
