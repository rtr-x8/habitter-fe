<template>
  <div>
    <p v-for="(provider, i) in providers" :key="i">
      <v-btn
        large
        block
        :href="redirectUrl(provider.name)"
        style="text-transform:capitalize"
        :color="provider.color"
        :disabled="provider.disable"
      >
        {{ provider.name }}でログイン
      </v-btn>
    </p>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      providers: [
        {
          name: 'twitter',
          color: '#1DA1F2',
          disable: false
        },
        {
          name: 'github',
          color: '#24292E',
          disable: true
        }
      ]
    }
  },
  methods: {
    redirectUrl (provider) {
      return '/oauth/redirect/' + provider
    }
  }
}
</script>
