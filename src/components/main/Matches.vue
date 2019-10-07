<template>
  <div flex-center class="main row">
    <h2 v-if="!matches" class="main__container col-11">Loading</h2>
    <section class="filters">
      <h3>Выберите матч</h3>
      <q-form class="filters__container">
        <q-select
          @input="filterActiv()"
          v-for="selector in filters"
          :value="selector.value"
          :key="selector.name"
          v-model="selector.value"
          :options="unique(selector.getter)"
          :label="selector.name"
          clearable
        >
          <template v-if="selector.value" v-slot:append>
            <q-icon name="cancel" @click.stop="selector.value = null" class="cursor-pointer" />
          </template>
        </q-select>
      </q-form>
    </section>
    <section>

    </section>
    <section v-if="filterActivated">
      <div
               v-for="match in filteredMatches"
               :key="match.id"
               class="matches col-11 row main__container">
        <div class="match match_id row ">
          <div class="match__data">
            <p>{{ match.sport }}</p>
            <p>{{ match.city }}</p>
            <p>{{ match.adress }}</p>
            <p>{{ match.date }}</p>
            <p>{{ match.time }}</p>
          </div>
          <div class="row">
            <section class="match__description col-md-10 col-sm-10 col-xs-11" >
              <h3>Описание матча</h3>
              <!-- <p>Услуги сервиса InCitySport бесплатные.</p> -->
              <p>Оплата игроками за аренду зала производится администратору зала непосредственно перед матчем. Оплату равномерно рассчитывают сами игроки исходя из количества игроков и цены аренды зала. Для данного матча цена участия для одного игрока составит <strong>от 30-ти до 60-ти рублей</strong>.</p>
            </section>
          </div>
          <section class="teams">
            <team1 :match="match" :matchIndex="match.id"/>
            <team2 :match="match" :matchIndex="match.id"/>
            <team3 :match="match" :matchIndex="match.id"/>
          </section>
          <sendMail :match="match"/>
        </div>
      </div>
    </section>

  </div>
</template>

<script>
import Team1 from 'components/main/Team1.vue'
import Team2 from 'components/main/Team2.vue'
import Team3 from 'components/main/Team3.vue'
import sendMail from 'components/main/sendMail.vue'

export default {
  // props: ['match'],
  components: {
    Team1,
    Team2,
    Team3,
    sendMail
  },
  data () {
    return {
      filterActivated: false,
      email: null,
      filters: [
        { name: 'Sport', value: '', getter: obj => obj.sport },
        { name: 'City', value: '', getter: obj => obj.city },
        { name: 'Adress', value: '', getter: obj => obj.adress }
      ],
      emailRules: [
        v => !!v || 'Заполните поле',
        v => /.+@.+/.test(v) || 'Неверный формат',
        v => (v && v.length >= 8) || 'Минимальное количество символов - 8'
      ]
    }
  },
  methods: {
    filterActiv () {
      this.filterActivated = true
      // return this.filterActivated
    },
    unique (getter) {
      let matchesArray = this.matches
      return [...new Set(matchesArray.map(getter))]
      // return [...new Set(matches.map(obj => obj.city))]
    }
  },
  computed: {
    matches () {
      return this.$store.getters['module1/getMatches'].matchesUpdated
    },
    filteredMatches () {
      return this.filters.reduce((matches, { value, getter }) => {
        if (value) {
          return matches.filter(match => getter(match) === value)
        } else {
          return matches
        }
      }, this.matches)
    }
  },
  beforeCreate () {
    this.$store.dispatch('module1/getMatches')
  },
  created () {
    let now = Date.now()
    let expirationDate = localStorage.getItem('expirationDate')
    if (expirationDate !== null && now < expirationDate) {
      console.log('disable btn')
      this.$store.dispatch('module1/globalBtnsDisable')
    }
  }
}
</script>

<style lang="stylus" scoped>
  .main__container
    max-width: 1100px
    margin: 0 auto
    h3
      color: $primary
      margin: 20px auto 0
  .match
    border: 1px solid $color-main
    margin-bottom: 70px
    padding: 10px
  .match__description
    margin: 0 auto 30px
  .match__data
    width: 100%
    display: flex
    flex-wrap: wrap
    justify-content: center
    background: lightgrey
    p
      display: flex
      margin: auto
      font-weight: bold
      height: 40px
      justify-content: center
      text-align: center
      align-self: center
      align-items: center
      width: 15%
      min-width: 130px
  .teams
    width: 100%
    display: flex
    justify-content: space-between
  .filters
    color: $primary
    width: 100%
    background: linear-gradient(to right, lighten(#fff, 0%), lighten(#fff, 0%))
    background-size: cover
  .filters__container
    color: #fff
    margin: 0px auto 40px
    width: 50%
  .q-field__label
    color: #fff
  .team
    width: 30%
  .btn
    display: flex
    margin: 10px auto
  .match__sender
    margin: 30px auto 0
    border-top: 2px dashed $primary
    p
      padding: 10px
</style>
