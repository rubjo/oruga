<template>
  <main
    class="home"
    :aria-labelledby="data.heroText !== null ? 'main-title' : null"
  >
    <header class="hero">

      <img
        v-if="data.heroImage"
        :src="$withBase(data.heroImage)"
        :alt="data.heroAlt || 'hero'"
      >

      <h1
        v-if="data.heroText !== null"
        id="main-title"
      >
        {{ data.heroText || $title || 'Hello' }}
      </h1>

      <p
        v-if="data.tagline !== null"
        class="description"
      >
        {{ data.tagline || $description || 'Welcome to your VuePress site' }}
      </p>

      <p
        v-if="data.actionText && data.actionLink"
        class="action"
      >
        <NavLink
          class="action-button"
          :item="actionLink"
        />
      </p>

      <div class="ads-centered">
        <CarbonAds />
      </div>

      <div class="versions">
        <div class="version">
          <h2>Vue 2 version</h2>
          v.{{pkg.version}}
        </div>
        <div class="version changelog">
          <h2>
            <a href="https://github.com/oruga-ui/oruga/releases">
              Changelog
            </a>
          </h2>
        </div>
        <div class="version">
          <h2>Vue 3 version</h2>
          v.{{pkgNext.version}}
        </div>
      </div>

      <p align="center">
        <a href="https://ko-fi.com/orugaui">
          <img style="min-width:32px;height:32px;" src="https://github.githubassets.com/images/modules/site/icons/funding_platforms/ko_fi.svg" />Buy us a coffee ☕️
        </a>
      </p>

    </header>

    <div
      v-if="data.features && data.features.length"
      class="features"
    >
      <div
        v-for="(feature, index) in data.features"
        :key="index"
        class="feature"
      >
        <h2>{{ feature.title }}</h2>
        <p>{{ feature.details }}</p>
      </div>
    </div>

    <Content class="theme-default-content custom" />

    <div
      v-if="data.footer"
      class="footer"
    >
      {{ data.footer }}
    </div>
  </main>
</template>

<script>
import NavLink from '@theme/components/NavLink.vue'
import CarbonAds from '@theme/components/CarbonAds.vue'


import pkg from '../../../../oruga/package.json'
import pkgNext from '../../../../oruga-next/package.json'

export default {
  name: 'Home',

  components: { NavLink, CarbonAds },

  data() {
    return {
      pkg,
      pkgNext
    }
  },

  computed: {
    data () {
      return this.$page.frontmatter
    },

    actionLink () {
      return {
        link: this.data.actionLink,
        text: this.data.actionText
      }
    }
  }
}
</script>

<style lang="stylus">
.ads-centered
  display: flex
  justify-content: center
  margin-bottom: 2rem
.home
  padding $navbarHeight 2rem 0
  max-width $homePageWidth
  margin 0px auto
  display block
  .hero
    text-align center
    img
      max-width: 100%
      max-height 280px
      display block
      margin 1rem auto 0
    h1
      font-size 3rem
    .description, .action
      margin 1.8rem auto
    .description
      max-width 35rem
      font-size 1.6rem
      line-height 1.3
      color lighten($textColor, 40%)
    .action-button
      display inline-block
      font-size 1.2rem
      color #fff
      background-color $accentColor
      padding 0.8rem 1.6rem
      border-radius 4px
      transition background-color .1s ease
      box-sizing border-box
      border-bottom 1px solid darken($accentColor, 10%)
      &:hover
        background-color lighten($accentColor, 10%)
  .features
    border-top 1px solid $borderColor
    padding 1.2rem 0
    margin-top 1.5rem
    display flex
    flex-wrap wrap
    align-items flex-start
    align-content stretch
    justify-content space-between
  .feature
    flex-grow 1
    flex-basis 30%
    max-width 30%
    h2
      font-size 1.4rem
      font-weight 500
      border-bottom none
      padding-bottom 0
      color lighten($textColor, 10%)
    p
      color lighten($textColor, 25%)
  .versions
    display flex
    flex-wrap wrap
    align-items flex-start
    align-content stretch
    justify-content space-between
    color lighten($textColor, 10%)
    .version
      flex-grow 1
      flex-basis 30%
      color lighten($textColor, 25%)
      h2
        font-size 1.1rem
        font-weight 500
        border-bottom none
        padding 0
        margin 0
        color lighten($textColor, 10%)
  .footer
    padding 2.5rem
    border-top 1px solid $borderColor
    text-align center
    color lighten($textColor, 25%)

@media (max-width: $MQMobile)
  .home
    .features
      flex-direction column
    .feature
      max-width 100%
      padding 0 2.5rem
    .versions
      flex-direction column
    .version
      width 100%;
      padding .5rem
    .changelog
      order 2

@media (max-width: $MQMobileNarrow)
  .home
    padding-left 1.5rem
    padding-right 1.5rem
    .hero
      img
        max-height 210px
        margin 2rem auto 1.2rem
      h1
        font-size 2rem
      h1, .description, .action
        margin 1.2rem auto
      .description
        font-size 1.2rem
      .action-button
        font-size 1rem
        padding 0.6rem 1.2rem
    .feature
      h2
        font-size 1.25rem
</style>
