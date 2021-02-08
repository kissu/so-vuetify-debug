<template>
  <div>
    <v-form :model="user">
      <v-text-field
        label="First Name"
        @keydown.enter="focusNext"
        data-index="0"
        ref="input-0"
        v-model="user.first_name"
      >
      </v-text-field>

      <v-text-field
        data-index="1"
        ref="input-1"
        label="Last Name"
        v-model="user.last_name"
        @keydown.enter="focusNext"
      >
      </v-text-field>

      <v-select
        :items="cities"
        data-index="2"
        ref="input-2"
        attach
        item-text="name"
        item-value="name"
        v-model="user.city"
        label="City"
      >
      </v-select>

      <v-text-field
        data-index="2"
        ref="input-2"
        label="Phone Number"
        v-model="user.phone_number"
        @keydown.enter="focusNext"
      >
      </v-text-field>
    </v-form>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      user: {
        first_name: "",
        last_name: "",
        city: [],
        phone_number: "",
      },
      cities: ["a", "b", "c"],
    };
  },
  methods: {
    focusNext(event) {
      console.log("event", event);
      if (event.target) {
        const nextElement = this.$refs?.[
          `input-${Number(event.target.dataset.index) + 1}`
        ];
        if (nextElement) nextElement.focus();
      }
    },
  },
  watch: {
    "user.city"(newValue) {
      console.log("changed", newValue);
      this.focusNext();
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
