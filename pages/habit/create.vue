<template>
  <v-form
    ref="form"
    v-model="valid"
    :lazy-validation="lazy"
  >
    <v-text-field
      v-model="title"
      :counter="10"
      name="title"
      :rules="[v => !!v || 'title is required']"
      label="title"
      required
    />

    <v-checkbox
      v-model="checkbox"
      :rules="[v => !!v || 'You must agree to continue!']"
      label="Publish?"
      name="publish"
      required
    />

    <v-btn
      color="success"
      class="mr-4"
      @click="submit"
    >
      Submit
    </v-btn>
  </v-form>
</template>

<script>
export default {
  middleware: 'auth',
  data: () => ({
    valid: true,
    title: '',
    publish: '',
    checkbox: false,
    lazy: false
  }),

  methods: {
    async submit () {
      try {
        const data = await this.$axios.post('/habit/store', {
          title: this.title,
          publish: !!this.publish
        })

        // eslint-disable-next-line no-console
        console.log(data.data)
      } catch (error) {
        this.failedMessage = error.message
      }
    }
  }
}
</script>
