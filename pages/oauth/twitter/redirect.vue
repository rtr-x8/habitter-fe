<template>
  <p>Twitterへリダイレクトしています</p>
</template>

<script>
export default {
  middleware: 'guest',
  name: 'OauthTwitterRedirect',
  asyncData ({ app, error }) {
    return app.$axios.$get('/oauth/twitter/redirect')
      .then((data) => {
        console.log(data)
        return { twitterAuthUrl: data.redirect_url }
      })
      .catch(e => error({ message: e.message, statusCode: e.statusCode }))
  },
  data: () => {
    return {
      twitterAuthUrl: ''
    }
  },
  mounted () {
    // window.location.href = this.twitterAuthUrl
    // eslint-disable-next-line no-console
    console.log(this.twitterAuthUrl)
  }
}
</script>
