<template>
  <div class="banner">
    <div class="banner__slide">
      <div class="banner__slide-carousel">
        <!-- item 1  -->
        <div
          :class="{ carousel__item: true, hidden: this.active[0] }"
          style="
            background: url('https://user-images.githubusercontent.com/66562512/110658753-8945fa00-81f4-11eb-8f8a-acfc716de549.png')
              center no-repeat;
          "
        >
          <div class="container">
            <div class="carousel__item-wraper">
              <div class="wraper__content">
                <h6>fruit fresh</h6>
                <h1 :class="{ show: !this.active[0] }">orange lemon</h1>
                <h3 :class="{ show: !this.active[0] }">
                  16,00 US$ / <span>pakage</span>
                </h3>
                <router-link :to="{ name: 'foods' }">
                  <button :class="{ show: !this.active[0] }">
                    shop now
                  </button></router-link
                >
              </div>
              <div :class="{ wraper__image: true, show: !this.active[0] }">
                <img
                  src="https://user-images.githubusercontent.com/66562512/110657538-7d0d6d00-81f3-11eb-9791-a4be14873fb2.png"
                  alt=""
                />
              </div>
            </div>
          </div>
        </div>

        <!-- item 2 -->
        <div
          :class="{ carousel__item: true, hidden: this.active[1] }"
          style="
            background: url('https://user-images.githubusercontent.com/66562512/110658756-8a772700-81f4-11eb-9183-b52c74aee885.png')
              center no-repeat;
          "
        >
          <div class="container">
            <div class="carousel__item-wraper">
              <div class="wraper__content">
                <h6>butter & eggs</h6>
                <h1 :class="{ show: !this.active[1] }">spice 100% oganic</h1>
                <h3 :class="{ show: !this.active[1] }">
                  12,59 US$ / <span>pakage</span>
                </h3>
                <router-link :to="{ name: 'foods' }">
                  <button :class="{ show: !this.active[1] }">
                    shop now
                  </button></router-link
                >
              </div>
              <div :class="{ wraper__image: true, show: !this.active[1] }">
                <img
                  src="https://user-images.githubusercontent.com/66562512/110657538-7d0d6d00-81f3-11eb-9791-a4be14873fb2.png"
                  alt=""
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="banner__button">
      <button class="banner__button-previous" @click.prevent="handlePrevious">
        <i class="fas fa-angle-left"></i>
      </button>
      <button class="banner__button-next">
        <i class="fas fa-angle-right" @click.prevent="handleNext"></i>
      </button>
    </div>
    <benefits />
  </div>
</template>

<script>
import Benefits from "@/components/Benefits.vue";
export default {
  components:{Benefits},
  name: "banner",
  data() {
    return {
      slides: 2,
      position: 0,
      active: [true, false],
    };
  },
  methods: {
    handlePrevious() {
      this.position = this.position - 1;
      if (this.position < 0) {
        this.position = this.slides - 1;
      }
      this.isSlideActive(this.position);
    },
    handleNext() {
      this.position = this.position + 1;
      if (this.position === this.slides) {
        this.position = 0;
      }
      this.isSlideActive(this.position);
    },
    isSlideActive(position) {
      for (let index = 0; index < this.active.length; index++) {
        this.active[index] = false;
      }
      this.active[position] = true;
    },
  },
  mounted() {},
  watch: {},
};
</script>

