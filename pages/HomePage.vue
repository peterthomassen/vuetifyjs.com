<template lang="pug">
  div#home
    v-jumbotron(
      dark
      gradient="to bottom, #1867c0, #5CBBF6"
      height="auto"
    )
      a(
        class="chip v-chip--tidelift white--text"
        href="http://tidelift.com/subscription/npm/vuetify"
        rel="noopener"
        target="_blank"
        @click="$ga.event('home sponsor click', 'click', 'Tidelift')"
      )
        span.chip__content
          img(
            alt="Tidelift"
            class="mr-3"
            src="/static/doc-images/affiliates/tidelift-small.png"
            width="24px"
          )
          span.body-2.hidden-sm-and-down GET PROFESSIONALLY SUPPORTED VUETIFY
          span.body-2.hidden-md-and-up GET PROFESSIONAL SUPPORT
      v-container(fill-height).mt-3.mb-3
        v-layout(
          align-center
          justify-center
          wrap
        )
          img(
            src="/static/vuetify-logo-300.png"
            alt="Logo"
            style="logoStyles"
            height="256px"
            width="256px"
          ).mx-4
          v-flex(shrink).text-xs-center.text-md-left
            h1(
              class="mb-4"
              style="font-weight: 300;"
              :class="{ 'display-1 mt-4': isBooted && $vuetify.breakpoint.xsOnly }"
            ).display-3
              div(v-text="$t('Vuetify.Home.materialDesign')")
              div(v-text="$t('Vuetify.Home.componentFramework')")
            v-btn(
              :to="{ name: 'getting-started/QuickStart' }"
              class="primary--text"
              color="white"
              large
              style="min-width: 128px;"
            )
              | {{ $t("Vuetify.Home.getStarted") }}
            v-btn(
              color="white"
              href="https://github.com/vuetifyjs/vuetify"
              large
              outline
              rel="noopener"
              target="_blank"
            )
              v-icon(left) mdi-github-circle
              | Github
            v-btn(
              color="white"
              href="https://community.vuetifyjs.com"
              large
              outline
              rel="noopener"
              target="_blank"
            )
              v-icon(left) mdi-discord
              | {{ $t("Vuetify.Home.getHelp") }}

      v-container(
        grid-list-xl
        style="max-width: 1280px"
      ).mb-5
        v-layout(row wrap justify-center)
          v-flex(
            d-flex
            xs12 sm6 md4 lg4
            v-for="(feature, i) in features"
            :key="feature.title"
          )
            v-card(
              light
              style="max-width: 375px;"
            ).elevation-24.hide-overflow
              img(
                :src="feature.img"
                width="100%"
              ).mb-2
              v-card-text
                h3(
                  v-text="feature.title"
                  style="font-size: 18px; font-weight: 500;"
                ).mb-3.text-xs-center
                p(v-text="feature.text").text-xs-center.mb-2

    section#sponsors-and-backers.my-5
      v-container
        v-layout
          v-flex(xs12)
            h2(v-text="$t('Vuetify.Home.proudlySponsoredBy')").text-xs-center.headline.mb-3.grey--text
            v-layout(row wrap justify-center align-center)
              template(v-for="(supporter, i) in supporters")
                v-flex(
                  xs12
                  v-if="supporter.break"
                  :key="i"
                ) &nbsp;
                a(
                  target="_blank"
                  rel="noopener"
                  class="ma-3"
                  :href="`${supporter.href}?ref=vuetifyjs.com`"
                  :title="supporter.title"
                  :key="i"
                  @click="$ga.event('home sponsor click', 'click', supporter.title)"
                  v-else
                )
                  img(
                    :src="`/static/doc-images/${supporter.src}`"
                    :height="supporter.size || 'auto'"
                    :style="{ maxHeight: `${supporter.size}px` }"
                  )
              v-flex(xs12).text-xs-center.mt-3
                v-btn(
                  :to="{ name: 'getting-started/SponsorsAndBackers' }"
                  color="primary"
                  large
                  outline
                ) {{ $t("Vuetify.Home.becomeSponsor") }}
                  v-icon(right color="primary") chevron_right

    section#checked-features.mb-5
      v-container
        h2.text-xs-center.headline.mb-5.grey--text
          span {{ $t("Vuetify.Home.checkFeaturesTitle") }}
          | {{ $t("Vuetify.Home.checkFeaturesTitleCtd") }}
        v-layout(row wrap justify-center)
          v-flex(
            mx-3
            :shrink="$vuetify.breakpoint.mdAndUp"
            :grow="$vuetify.breakpoint.smAndDown"
          )
            v-layout(
              v-for="(feature, i) in checkFeatures"
              :key="i"
              align-center
            ).my-2
              v-icon(
                color="green"
                size="36px"
              ).mr-3 check
              span.subheading {{ feature }}
          v-flex(
            mx-3
            :shrink="$vuetify.breakpoint.mdAndUp"
            :grow="$vuetify.breakpoint.smAndDown"
          )
            v-layout(
              v-for="(feature, i) in checkFeaturesCtd"
              :key="i"
              align-center
            ).my-2
              v-icon(
                color="green"
                size="36px"
              ).mr-3 check
              span.subheading {{ feature }}

    section#using-vuetify.mb-5
      v-container(grid-list-xl)
        h2.text-xs-center.headline.mb-5.grey--text
          span {{ $t("Vuetify.Home.madeWithVuetify") }}
        v-layout(wrap)
          v-flex(
            v-for="(feature, i) in computedFeatured"
            :key="i"
            xs12
            sm6
            md4
          )
            v-card(
              :href="`${feature.url}?ref=vuetifyjs.com`"
              :img="feature.image"
              height="300px"
              target="_blank"
              rel="noopener"
              @click="$ga.event('home mwvjs click', 'click', feature.title)"
            ).elevation-24
        v-layout(
          justify-center
          pt-3
        )
          a(
            href="https://madewithvuejs.com?ref=vuetifyjs.com"
            target="_blank"
            rel="noopener"
            @click="$ga.event('home mwvjs click', 'click', 'madewithvuejs')"
          )
            img(
              src="/static/doc-images/powered-by-madewithvue-1.svg"
              height="65px"
            )

    v-jumbotron(
      dark
      gradient="to top, #1867c0, #5CBBF6"
      height="auto"
    )
      v-container.mt-4.mb-3
        v-layout(row wrap)
          v-flex(xs12)
            h5.mb-3
              v-layout(align-center justify-center column)
                img(
                  src="/static/v-alt.svg"
                  height="64px"
                  width="64px"
                ).mb-2
                span(v-text="$t('Vuetify.Home.callout')").subheading

        v-layout(justify-center).mb-3
          a(
            v-for="(social, i) in socials"
            :href="social.href"
            :key="i"
            :title="social.title"
            target="_blank"
            rel="noopener"
          ).social.mx-3
            v-icon(v-text="social.icon")

        v-layout(column text-xs-center)
          div Released under the&nbsp;
            a(
              href="https://opensource.org/licenses/MIT"
              rel="noopener"
              style="text-decoration: none;"
              target="_blank"
              v-text="$t('Vuetify.Home.mit')"
            ).body-2.white--text
          div Copyright &copy; 2016-{{ (new Date()).getFullYear() }} Vuetify, LLC
</template>

<script>
  import supporters from '@/assets/supporters'

  // Mixins
  import Message from '@/mixins/message'

  export default {
    name: 'HomePage',

    mixins: [Message],

    data: () => ({
      diamond: supporters.diamond,
      featured: [],
      isBooted: false,
      palladium: supporters.palladium,
      socials: [
        {
          icon: 'mdi-reddit',
          href: 'https://www.reddit.com/r/vuetifyjs',
          title: 'Reddit'
        },
        {
          icon: 'mdi-medium',
          href: 'https://medium.com/vuetify',
          title: 'Medium'
        },
        {
          icon: 'mdi-github-circle',
          href: 'https://github.com/vuetifyjs/vuetify',
          title: 'Github'
        },
        {
          icon: 'mdi-twitter',
          href: 'https://twitter.com/vuetifyjs',
          title: 'Twitter'
        },
        {
          icon: 'mdi-facebook',
          href: 'https://www.facebook.com/vuetifyjs',
          title: 'Facebook'
        },
        {
          icon: 'mdi-discord',
          href: 'https://community.vuetifyjs.com',
          title: 'Discord Community'
        }
      ]
    }),

    computed: {
      checkFeatures () {
        return this.$t('Vuetify.Home.checkFeatures')
      },
      checkFeaturesCtd () {
        return this.$t('Vuetify.Home.checkFeaturesCtd')
      },
      computedFeatured () {
        return this.featured.slice(0, 6)
      },
      features () {
        return this.$t('Vuetify.Home.features').slice().reverse()
      },
      letterFromAuthor () {
        return this.$t('Vuetify.Home.letterFromAuthor')
      },
      supporters () {
        const supporters = [...this.diamond, ...this.palladium]

        const end = { break: true }

        supporters.splice(3, 0, end)

        return supporters
      }
    },

    async mounted () {
      await this.$nextTick()
      this.isBooted = true

      this.$http({
        method: 'GET',
        url: 'https://madewithvuejs.com/api/tag/vuetify',
        headers: {
          'Access-Control-Allow-Origin': '*',
          'Content-Type': 'application/json'
        }
      })
        .then(res => {
          this.featured = this.setFeatured(res.data)
        })
        .catch(err => console.log(err))
    },

    methods: {
      setFeatured (data) {
        if (!data) return []

        const featured = data.data.map(f => {
          f.hover = false

          return f
        })

        return this.shuffle(featured)
      },
      shuffle (array) {
        let currentIndex = array.length
        let temporaryValue
        let randomIndex

        // While there remain elements to shuffle...
        while (currentIndex !== 0) {
          // Pick a remaining element...
          randomIndex = Math.floor(Math.random() * currentIndex)
          currentIndex -= 1

          // And swap it with the current element.
          temporaryValue = array[currentIndex]
          array[currentIndex] = array[randomIndex]
          array[randomIndex] = temporaryValue
        }

        return array
      },
      snackHandler () {
        this.$router.push({ name: 'store/Index' })
      }
    }
  }
</script>

<style lang="stylus" scoped>
  .social
    text-decoration: none

  .v-chip--tidelift
    background: #f6914d !important
    padding-right: 64px
    position: absolute
    right: -24px
    text-decoration: none
    top: -20px

    .chip__content
      cursor: pointer !important
</style>
