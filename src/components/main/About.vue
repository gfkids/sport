<template>
  <section class="about row">
    <div class="about__container row col-11">
      <section class="about__desc col-sm-8 col-xs-12 col-md-5 col-lg-6 col-xl-6">
        <h2>Описание сервиса</h2>
        <p>Не всегда получается собрать несколько команд для игры в футбол. Вы можете принять участие в любительской игре, не собирая команду. </p>
        <p>Забронируйте место в команде из таких же как Вы активных игроков-любителей в подходящем для Вас матче и приходите на матч.</p>
        <p>Услуги сервиса бесплатные, игрок платит только свою долю аренды зала на матч (от 30-ти до 60-ти рублей).</p>
      </section>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  computed: {
  },
  methods: {
  }
}
</script>

<style lang="stylus">
  .about
    display: flex
    min-height: 350px
    background: linear-gradient(to right, rgba(0, 0, 0, 0.8) 40%, rgba(0, 0, 0, 0.0) ), url('../../statics/img/hit.png') no-repeat 70% center
    background: url('../../statics/img/players.jpg') no-repeat 80% center
    background-size: 30% auto
    @media (max-width $breakpoint-xs-max)
      background: linear-gradient(rgba(0, 0, 0, 0.5) 50%, rgba(0, 0, 0, 0.5) ), url('../../statics/img/football-220kb.jpg') no-repeat
      background-size: cover

    h2
      color: #fff
      color: $primary
      margin-top: 0
      display: block
    p
      display: block
      padding: 0
      color: #fff
      color: $gray
      margin-bottom: 8px
      font-size: $font-size-h5
      line-height: $line-height-h5
  .about__container
    border-left: 3px solid $primary
    padding: 0 10px
    max-width: 1100px
    margin: 20px auto
  .about__desc
    display: flex
    flex-direction: column
    justify-content: space-around
</style>
