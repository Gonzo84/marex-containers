<template>
    <div class="root">
        <div class="parallax">
            <hexagonal />
        </div>
        <v-container class="fixed-width">
            <v-row class="spacing6">
                <v-col md="6" class="pa-6">
                    <title-main :align="isMobile ? 'center' : 'left'" :head="'FAQ'" />
                    <p
                        class="use-text-subtitle2"
                        :class="[isMobile ? 'text-center' : 'text-left']"
                    >
                        {{ $t('architectLanding.faq_subtitle') }}
                    </p>
                    <hidden point="smDown">
                        <div class="illustration">
                            <img src="/images/containers/faq.png" alt="illustration">
                        </div>
                    </hidden>
                </v-col>
                <v-col md="6" cols="12" class="pa-6">
                    <div class="accordion">
                        <v-expansion-panels
                            v-model="panel"
                            variant="accordion"
                            active-class="expanded"
                        >
                            <v-expansion-panel
                                v-for="(item, index) in faqData"
                                :key="index"
                                class="paper"
                            >
                                <v-expansion-panel-title class="content">
                                    <p class="heading">
                                        {{ item.q }}
                                    </p>
                                </v-expansion-panel-title>
                                <v-expansion-panel-text class="detail">
                                    <p>
                                        {{ item.a }}
                                    </p>
                                </v-expansion-panel-text>
                            </v-expansion-panel>
                        </v-expansion-panels>
                    </div>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<style lang="scss" scoped>
@import 'faq-style.scss';
</style>

<script>
import Hidden from '../Hidden';
import Hexagonal from '../Parallax/Hexagonal';
import Title from '../Title';

export default {
    components: {
        Hidden,
        Hexagonal,
        'title-main': Title,
    },
    data() {
        return {
            panel: 0,
            faqData: [
                {
                    q: this.$t('faq.question1'),
                    a: this.$t('faq.answer1'),
                },
                {
                    q: this.$t('faq.question2'),
                    a: this.$t('faq.answer2'),
                }, {
                    q: this.$t('faq.question3'),
                    a: this.$t('faq.answer3'),
                }, {
                    q: this.$t('faq.question4'),
                    a: this.$t('faq.answer4'),
                }, {
                    q: this.$t('faq.question5'),
                    a: this.$t('faq.answer5'),
                },
            ],
        };
    },
    computed: {
        isMobile() {
            const smDown = this.$vuetify.display.smAndDown;
            return smDown;
        },
    },
};
</script>
