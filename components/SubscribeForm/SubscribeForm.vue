<template>
  <div class="root">
    <div class="bg-deco">
      <img :src="imgAPI.containers[4]" alt="3d home model">
    </div>
    <div class="parallax-wrap">
      <v-parallax
        :src="imgAPI.architect[15]"
        :height="570"
      />
    </div>
    <v-container class="fixed-width">
      <v-card class="form">
        <h4 class="use-text-title2">
          {{ $t('architectLanding.subscribe_title') }}
        </h4>
        <p class="use-text-subtitle2">
          {{ $t('architectLanding.subscribe_subtitle') }}
        </p>
        <NuxtLink :to="link.architect.contact">
          <v-btn size="large" color="secondary" class="button mt-4">
              {{ $t('architectLanding.banner_btn') }}
          </v-btn>
        </NuxtLink>
      </v-card>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './subscribe-style.scss';
</style>

<script>
import imgAPI from '@/assets/images/imgAPI';
import link from '@/assets/text/link';

export default {
  data: () => ({
    imgAPI,
    link,
  }),
};
</script>
