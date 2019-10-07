<template>
  <div class="row">
    <section class="match__sender col-10">
      <p>Вы можете подписаться на все матчи, открываемые по этому адресу и не пропустить свободные места. Вы будете получать информацию о каждом матче сразу после открытия регистрации на него.</p>
      <q-form  @submit="onSubmit">
        <q-input
          type="email"
          :rules="emailRules"
          label="Электронная почта *"
          v-model='email'
        />
        <q-btn color="primary"
          type="Submit"
          class="btn"
          label="Подписаться"/>
      </q-form>
    </section>
  </div>
</template>

<script>
export default {
  props: ['match'],
  data () {
    return {
      email: null,
      emailRules: [
        v => !!v || 'Заполните поле',
        v => /.+@.+/.test(v) || 'Неверный формат',
        v => (v && v.length >= 8) || 'Минимальное количество символов - 8'
      ]
    }
  },
  computed: {
  },
  methods: {
    onSubmit () {
      let mailData = {
        email: this.email,
        matchData: {
          city: this.match.city,
          adress: this.match.adress,
          sport: this.match.sport
        }
      }
      console.log(this.match)
      console.log(mailData)
      this.$store.dispatch('module1/sendMail', mailData)
      this.$q.notify({
        color: 'green-4',
        textColor: 'white',
        icon: 'cloud_done',
        message: 'Вы подписаны на уведомления о матчах.'
      })
    }
  }
}
</script>

<style lang="stylus" scoped>
.match__sender
  margin: 30px auto 0
  border-top: 2px dashed $primary
  p
    padding: 10px
</style>
