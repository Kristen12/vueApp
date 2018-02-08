<template>
    <div class="book-box">
        <swipe class="my-swipe">
            <swipe-item class="slide1"><img src="../../assets/images/1.png" alt=""></swipe-item>
            <swipe-item class="slide2"><img src="../../assets/images/2.png" alt=""></swipe-item>
            <swipe-item class="slide3"><img src="../../assets/images/3.png" alt=""></swipe-item>
        </swipe>
    </div>
</template>

<script>
// require('vue-swipe/dist/vue-swipe.css');
import vueswipe from "vue-swipe/dist/vue-swipe.css";
import { Swipe, SwipeItem } from "vue-swipe";
export default {
  mounted: function() {
    this.$store.commit("change", {
      bgColor: "#1f1f1f",
      title: "Book"
    });
  },
  components: {
    Swipe,
    SwipeItem
  }
};
</script>

<style scoped>
.my-swipe {
  height: 4.15rem;
}
.my-swipe img{
    height:4.15rem;
}

.slide1 {

}

.slide2 {

}

.slide3 {
 
}
</style>