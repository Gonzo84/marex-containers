<template>
  <div class="root">
    <v-container :class="{fixed: !isMobile}" class="banner-wrap">
      <div class="video">
        <div class="overlay" />
        <!--        <img v-if="!play || isMobile" :src="imgAPI.architect[0]" alt="cover">-->
        <video src="@/assets/videos/BackgroundVideo_Homepage.mp4" autoplay muted loop />
      </div>
      <div class="parallax">
        <cross-parallax />
      </div>
      <div class="block">
        <v-row justify="end">
          <v-col md="9" cols="12">
            <div class="paper-wrap">
              <v-card class="paper">
                <div>
                  <h4 class="use-text-title2">
                    {{ $t('architectLanding.banner_title') }}
                  </h4>
                  <p class="subtitle use-text-subtitle2">
                    {{ $t('architectLanding.banner_desc') }}
                  </p>
                  <NuxtLink :to="link.architect.contact">
                    <v-btn size="large" color="primary" class="button">
                      {{ $t('architectLanding.banner_btn') }}
                    </v-btn>
                  </NuxtLink>
                </div>
              </v-card>
            </div>
          </v-col>
        </v-row>
      </div>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './banner-style.scss';
</style>

<script>

import link from '@/assets/text/link';
import imgAPI from '@/assets/images/imgAPI';
import CrossParallax from '../Parallax/Cross';

export default {
  components: {
    CrossParallax,
  },
  data() {
    return {
      link,
      imgAPI,
      play: false,
      cover: imgAPI.architect[0],
    };
  },
  computed: {
    isDesktop() {
      const lgUp = this.$vuetify.display.lgAndUp;
      return lgUp;
    },
    isMobile() {
      const mdDown = this.$vuetify.display.mdAndDown;
      return mdDown;
    },
  },
};
</script>
