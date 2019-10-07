<template>
  <footer class="footer row">
    <div class="footer__content col-11">
      <div class="footer__logo">
        <router-link to="/"
           tag="p"
           >
          InCitySport
        </router-link>
      </div>
      <p>Cooperative sport</p>
    </div>
  </footer>
</template>

<script>

</script>

<style lang="stylus">
  .footer
    display: flex
    position: relative
    font-family: $font-base
    z-index: 3
    background-color: #fff
    color: $primary
    border-top: 1px solid $color-dark
    margin-top: auto
    height: 50px
  .footer__content
    display: flex
    justify-content: space-between
    margin: auto
    p
      display: block
      align-self: center
      width: $col-9
      color: darken($primary, 20%)
      text-align: center
      font-weight: 400
      margin: auto
  .footer__logo
    display: flex
    width: 50px
    cursor: pointer
    p
      margin: auto
      font-style: italic
      font-size: $font-size-h4
      text-align: center

</style>
