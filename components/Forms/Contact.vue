<template>
  <div class="page-wrap">
    <hidden point="mdDown">
      <div class="bg-deco" />
    </hidden>
    <div class="parallax">
      <cross-parallax />
    </div>
    <v-snackbar
      v-model="snackbar"
      :timeout="4000"
      location="top right"
      class="notification"
    >
      <div class="action">
        Message Sent
      </div>
      <template #actions>
        <v-btn
          variant="text"
          icon
          @click="snackbar = false"
        >
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </template>
    </v-snackbar>
    <hidden point="mdUp">
      <div class="logo logo-header">
        <nuxt-link :to="routeLink.architect.home">
          <img :src="logo" alt="logo">
          <span class="use-text-title">
            {{ brand.architect.projectName }}
          </span>
        </nuxt-link>
      </div>
    </hidden>
    <v-container class="max-lg inner-wrap">
      <v-btn
        :to="localePath(routeLink.architect.home)"
        icon
        variant="text"
        class="backtohome"
      >
        <i class="ion-ios-home-outline" />
        <i class="ion-ios-arrow-round-back-outline" />
      </v-btn>
      <v-row>
        <v-col lg="1" cols="12" class="use-hidden-xs-down">
                    &nbsp;
        </v-col>
        <v-col lg="5" cols="12" class="wrap-deco">
          <hidden point="mdDown">
            <div class="frm-deco" />
          </hidden>
          <v-card class="form-box fragment-fadeUp">
            <div class="full-form-wrap">
              <div class="form">
                <title-main
                  :desc="$t('common.contact_subtitle')"
                  head="Contact Us"
                />
                <v-form
                  ref="form"
                  v-model="valid"
                  @submit.prevent="validateForm"
                >
                  <v-row class="spacing6">
                    <v-col cols="12" sm="12" class="px-6">
                      <v-text-field
                        v-model="name"
                        :rules="nameRules"
                        :label="$t('common.form_name')"
                        required
                        color="primary"
                        variant="underlined"
                      />
                    </v-col>
                    <v-col cols="12" sm="12" class="px-6">
                      <v-text-field
                        v-model="email"
                        :rules="emailRules"
                        :label="$t('common.form_email')"
                        required
                        color="primary"
                        variant="underlined"
                      />
                    </v-col>
                    <v-col cols="12" sm="12" class="px-6">
                      <v-text-field
                        v-model="phone"
                        :label="$t('common.form_phone')"
                        color="primary"
                        variant="underlined"
                      />
                    </v-col>
                    <v-col cols="12" sm="12" class="px-6">
                      <v-text-field
                        v-model="company"
                        :label="$t('common.form_company')"
                        color="primary"
                        variant="underlined"
                      />
                    </v-col>
                    <v-col cols="12" class="px-6">
                      <v-textarea
                        v-model="message"
                        :label="$t('common.form_message')"
                        rows="6"
                        color="primary"
                        variant="underlined"
                      />
                    </v-col>
                  </v-row>
                  <div class="form-control-label">
                    <v-checkbox
                      v-model="checkbox"
                      color="secondary"
                      :rules="[v => !!v || 'You must agree to continue!']"
                      :label="$t('common.form_terms')"
                      :hide-details="hideDetail"
                      required
                    />
                    <span>
                      <a href="#" class="link mx-3">
                        {{ $t('common.form_privacy') }}
                      </a>
                    </span>
                  </div>
                  <div class="btn-area">
                    <v-btn
                      :loading="loading"
                      :block="isMobile"
                      type="submit"
                      large
                      color="primary"
                    >
                      {{ $t('common.form_send') }}
                      <v-icon class="right-icon">
                        mdi-send
                      </v-icon>
                    </v-btn>
                  </div>
                </v-form>
              </div>
            </div>
          </v-card>
        </v-col>
        <v-col lg="6" cols="12">
          <hidden point="mdDown">
            <v-card class="map" raised>
              <GoogleMap
                api-key="AIzaSyAttq7XF6w9-AqGCXldh0KDu4s07DLIA88"
                :zoom="5"
                :center="{ lat: locations[0].lat, lng: locations[0].lng }"
                style="width: 100%; height: 100%"
              >
                <InfoWindow
                  :options="{ position: { lat: locations[0].lat + 1, lng: locations[0].lng } }"
                >
                  <div class="bubel">
                    <h6 class="use-text-subtitle pb-1 px-3">
                      Head Quarter
                    </h6>
                    <v-row class="ma-3">
                      <v-col item sm="6" cols="12">
                        <p>
                          <v-icon class="icon">
                            mdi-phone
                          </v-icon>
                          +44 333 038 3229
                        </p>
                      </v-col>
                      <v-col item sm="6" cols="12">
                        <p>
                          <v-icon class="icon">
                            mdi-email
                          </v-icon>
                          hello@boltcontainers.co.uk
                        </p>
                      </v-col>
                      <v-col item sm="12" cols="12">
                        <p>
                          <v-icon class="icon">
                            mdi-map-marker
                          </v-icon>
                          Our locations
                        </p>
                      </v-col>
                    </v-row>
                  </div>
                </InfoWindow>
                <MarkerCluster>
                  <Marker
                    v-for="(location, i) in locations"
                    :key="i"
                    :options="{ position: location }"
                  />
                </MarkerCluster>
              </GoogleMap>
            </v-card>
          </hidden>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './form-style.scss';
</style>

<script>
import {
  GoogleMap,
  Marker,
  MarkerCluster,
  InfoWindow,
} from 'vue3-google-map';
import logo from '@/assets/images/bolt-logo.png';
import brand from '@/assets/text/brand';
import routeLink from '@/assets/text/link';
import { useLocalePath } from '#imports';
import Title from '../Title';
import CrossParallax from '../Parallax/Cross';
import Hidden from '../Hidden';

export default {
  components: {
    'title-main': Title,
    CrossParallax,
    Hidden,
    GoogleMap,
    Marker,
    MarkerCluster,
    InfoWindow,
  },
  setup() {
    const localePath = useLocalePath();
    return {
      localePath,
    };
  },
  data: () => ({

    loading: false,
    currentLocation: {},
    locations: [
      {
        lat: 51.50280,
        lng: -0.11953,
      },
      {
        lat: 51.9617,
        lng: 1.3513,
      },
      {
        lat: 50.9138489,
        lng: -1.47843,
      },
      {
        lat: 53.3933368,
        lng: -3.0009889,
      },
      {
        lat: 56.0154147,
        lng: -3.7307377,
      },
    ],
    logo,
    brand,
    hideDetail: true,
    routeLink,
    valid: true,
    snackbar: false,
    name: '',
    nameRules: [v => !!v || 'Name is required'],
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    phone: '',
    company: '',
    message: '',
    checkbox: false,
  }),
  computed: {
    isMobile() {
      const smDown = this.$vuetify.display.smAndDown;
      return smDown;
    },
  },
  methods: {
    async validateForm() {
      this.loading = true;
      const { valid } = await this.$refs.form.validate();

      if (valid) {
        this.submitForm();
      } else {
        this.hideDetail = false;
      }

      this.loading = false;
    },
    async submitForm() {
      const data = {
        access_key: useRuntimeConfig().public.accessKey,
        subject: 'New Inquiry',
        name: this.name,
        email: this.email,
        phone: this.phone,
        company: this.company,
        message: this.message,
      };
      try {
        const response = await $fetch('https://api.web3forms.com/submit', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: data,
        });
        if (response.success) {
          this.snackbar = true;
          this.hideDetail = true;
        } else {
          console.log(response); // Log for debugging, can be removed
        }
      } catch (error) {
        console.log(error); // Log for debugging, can be removed
      } finally {
        // Reset form after submission
        this.name = '';
        this.email = '';
        this.message = '';
        this.company = '';
        this.phone = '';

        // Clear result and status after 5 seconds
        setTimeout(() => {
          this.snackbar = false;
        }, 5000);
      }

      this.loading = false;
    },
  },
};
</script>
