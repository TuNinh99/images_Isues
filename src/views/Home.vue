<template>
  <div class="home">
    <the-header />
    <router-view></router-view>
    <partner />
    <the-footer />
    <quick-view />
    <div :class="{ message: true, show: this.$store.state.showMessage }">
      <div class="message__check">
        <i class="fas fa-check"></i>
      </div>
      <div class="message__infor">{{ this.$store.state.message }}</div>
    </div>
    <button class="backTop" @click.prevent="scrollToTop">
      <i class="fas fa-long-arrow-alt-up"></i>
    </button>
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader.vue";
import TheFooter from "@/components/TheFooter.vue";
import QuickView from "@/components/QuickView.vue";
import Partner from "@/components/Partner.vue";

export default {
  name: "Home",
  components: {
    TheHeader,
    TheFooter,
    QuickView,
    Partner,
  },
  methods: {
    totalPay(cart) {
      const total = cart.reduce((total, item) => {
        total = total + Number(item.quantity) * Number(item.price);
        return total;
      }, 0);
      return total.toFixed(2);
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: "smooth" });
    },
  },
  created() {
    const keyValue = "cart";
    let check = 0;
    for (let i = 0; i < localStorage.length; i++) {
      let key = localStorage.key(i);
      if (key !== keyValue) {
        check++;
      }
    }
    if (check === localStorage.length) {
      localStorage.setItem("cart", []);
      this.cart = [];
      this.$store.state.totalPay = 0;
      this.$store.state.totalPay = (0).toFixed(2);
    } else {
      const cart = JSON.parse(localStorage.getItem("cart"));
      this.$store.state.totalPay = this.totalPay(cart);
    }
  },
  mounted() {
    const backTop = document.querySelector(".backTop");
    window.addEventListener("scroll", () => {
      window.pageYOffset > 200
        ? backTop.classList.add("show")
        : backTop.classList.remove("show");
    });
  },
};
</script>

