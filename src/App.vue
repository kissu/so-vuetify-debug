<template>
  <div>
    <v-form :model="user">
      <v-text-field
        @focus="resetCurrentIndex"
        label="First Name"
        @keydown.enter="focusNext"
        ref="input-0"
        v-model="user.first_name"
      >
      </v-text-field>

      <v-text-field ref="input-1" label="Last Name" v-model="user.last_name" @keydown.enter="focusNext">
      </v-text-field>

      <v-select
        :items="cities"
        ref="input-2"
        attach
        item-text="name"
        item-value="name"
        v-model="user.city"
        label="City"
      >
      </v-select>

      <v-text-field ref="input-3" label="Phone Number" v-model="user.phone_number" @keydown.enter="focusNext">
      </v-text-field>
    </v-form>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      user: {
        first_name: '',
        last_name: '',
        city: [],
        phone_number: '',
      },
      cities: ['tokyo', 'berlin', 'nairobi'],
      currentIndex: 0,
    }
  },
  methods: {
    resetCurrentIndex() {
      this.currentIndex = 0
    },
    focusNext(event) {
      console.log('event', event)
      this.currentIndex += 1
      const nextElement = this.$refs[`input-${this.currentIndex}`]
      if (nextElement) nextElement.focus()
    },
  },
  watch: {
    'user.city'(newValue) {
      console.log('changed', newValue)
      this.focusNext()
    },
  },
}
</script>
