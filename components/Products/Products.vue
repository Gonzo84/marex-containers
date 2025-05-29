<template>
  <div class="root">
    <v-container>
      <div class="slider-wrap">
        <transition-group
          :name="transition"
          tag="div"
        >
          <div
            v-for="number in [currentImg]"
            :key="number"
            class="slide slider-content"
          >
            <div class="inner item" :class="[ number % 2 ? 'even' : 'odd' ]">
              <div class="inner-bg">
                <v-row>
                  <v-col md="4" cols="12" class="pa-0">
                    <div class="text">
                      <hidden point="mdUp">
                        <div class="background">
                          <img :src="content[Math.abs(currentImg) % content.length].image" alt="promotion">
                        </div>
                      </hidden>
                      <h4 class="use-text-subtitle">
                        {{ content[Math.abs(currentImg) % content.length].title }}
                      </h4>
                      <h5 class="use-text-title">
                        <span class="use-text-subtitle2">
                          {{ content[Math.abs(currentImg) % content.length].subtitle }}
                        </span>
                      </h5>
                      <article class="desc">
                        <h6 class="use-text-paragraph">
                          {{ content[Math.abs(currentImg) % content.length].desc }}
                        </h6>
                      </article>
                      <NuxtLink :to="link.architect.contact">
                        <v-btn variant="outlined" class="button">
                          {{ $t('architectLanding.banner_btn') }}
                          <v-icon class="icon-btn">
                            mdi-arrow-right
                          </v-icon>
                        </v-btn>
                      </NuxtLink>
                    </div>
                  </v-col>
                  <v-col md="8" cols="12" class="pa-0">
                    <hidden point="smDown">
                      <div class="image">
                        <img :src="content[Math.abs(currentImg) % content.length].image" alt="promotion">
                      </div>
                    </hidden>
                  </v-col>
                </v-row>
              </div>
            </div>
          </div>
        </transition-group>
      </div>
      <a
        href="javascript:void(0)"
        class="prev"
        @click="prev"
      >
        <v-icon class="arrow-icon">mdi-arrow-left</v-icon>
      </a>
      <a
        href="javascript:void(0)"
        class="next"
        @click="next"
      >
        <v-icon class="arrow-icon ">mdi-arrow-right</v-icon>
      </a>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './promotion-style.scss';
</style>

<script>
import imgAPI from '@/assets/images/imgAPI';
import Hidden from '../Hidden';
import link from '@/assets/text/link';

export default {
  components: {
    Hidden,
  },
  data() {
    return {
      content: [
        {
          subtitle: this.$t('promotions.subtitle1'),
          title: this.$t('promotions.title1'),
          desc: this.$t('promotions.desc1'),
          image: imgAPI.containers[0],
        },
        {
          subtitle: this.$t('promotions.subtitle2'),
          title: this.$t('promotions.title2'),
          desc: this.$t('promotions.desc2'),
          image: imgAPI.containers[1],
        },
        {
          subtitle: this.$t('promotions.subtitle3'),
          title: this.$t('promotions.title3'),
          desc: this.$t('promotions.desc3'),
          image: imgAPI.containers[2],
        },
      ],
      transition: '',
      autoplay: null,
      currentImg: 0,
      link,
    };
  },
  mounted() {
    this.playSlider();
  },
  beforeUnmount() {
    clearInterval(this.autoplay);
  },
  methods: {
    playSlider() {
      this.autoplay = setInterval(() => {
        this.currentImg += 1;
        this.transition = 'slide-right';
      }, 10000);
    },
    manualPlay() {
      clearInterval(this.autoplay);
      setTimeout(() => {
        this.playSlider();
      }, 1);
    },
    next() {
      this.manualPlay();
      this.currentImg += 1;
      this.transition = 'slide-right';
    },
    prev() {
      this.manualPlay();
      this.currentImg -= 1;
      this.transition = 'slide-left';
    },
    swipeLeft() {
      this.next();
    },
    swipeRight() {
      this.prev();
    },
  },
};
</script>
