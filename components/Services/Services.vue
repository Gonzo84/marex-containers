<template>
  <div class="root">
    <v-container>
      <title-main
        :head="$t('architectLanding.services_title')"
        :desc="''"
      />
    </v-container>
    <v-container class="fixed-width">
      <v-row class="spacing8 grid">
        <v-col md="4" cols="12">
          <div class="figure">
            <img :src="imgAPI.containers[7]" alt="promotion">
          </div>
          <h5 class="use-text-subtitle2">
            {{ $t('architectLanding.services_item1') }}
          </h5>
          <p class="use-text-paragraph">
            {{ $t('architectLanding.services_itemdesc1') }}
          </p>
        </v-col>
        <v-col md="4" cols="12">
          <div class="figure">
            <img :src="imgAPI.containers[8]" alt="promotion">
          </div>
          <h5 class="use-text-subtitle2">
            {{ $t('architectLanding.services_item2') }}
          </h5>
          <p class="use-text-paragraph">
            {{ $t('architectLanding.services_itemdesc2') }}
          </p>
        </v-col>
        <v-col md="4" cols="12">
          <div class="figure">
            <img :src="imgAPI.containers[9]" alt="promotion">
          </div>
          <h5 class="use-text-subtitle2">
            {{ $t('architectLanding.services_item3') }}
          </h5>
          <p class="use-text-paragraph">
            {{ $t('architectLanding.services_itemdesc3') }}
          </p>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './services-style.scss';
</style>

<script>
import imgAPI from 'assets/images/imgAPI';
import Title from '../Title';

export default {
  components: {
    'title-main': Title,
  },
  data: () => ({
    imgAPI,
  }),
};
</script>
