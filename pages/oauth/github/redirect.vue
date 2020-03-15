<template>
  <p>Githubへリダイレクトしています</p>
</template>

<script>
export default {
  middleware: 'guest',
  name: 'OauthGithubRedirect',
  asyncData ({ app, error }) {
    return app.$axios.$get('/oauth/github/redirect')
      .then((data) => {
        return { githubAuthUrl: data.redirect_url }
      })
      .catch(e => error({ message: e.message, statusCode: e.statusCode }))
  },
  data: () => {
    return {
      githubAuthUrl: ''
    }
  },
  mounted () {
    // window.location.href = this.githubAuthUrl
    // eslint-disable-next-line no-console
    console.log(this.githubAuthUrl)
  }
}
</script>
