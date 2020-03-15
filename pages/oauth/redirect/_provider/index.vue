<template>
  <p>{{ provider }}へリダイレクトしています</p>
</template>

<script>
export default {
  middleware: 'guest',
  name: 'OauthRedirectProvider',
  validate ({ params }) {
    // 数値でなければならない
    return ['twitter', 'github'].includes(params.provider)
  },
  asyncData ({ app, error, params }) {
    return app.$axios.$get('/oauth/' + params.provider + '/redirect')
      .then((data) => {
        return {
          provierUrl: data.redirect_url,
          provider: params.provider
        }
      })
      .catch(e => error({
        message: e.message,
        statusCode: e.statusCode,
        provider: params.provider
      }))
  },
  data: () => {
    return {
      provierUrl: '',
      provider: ''
    }
  },
  mounted () {
    // window.location.href = this.provierUrl
    // eslint-disable-next-line no-console
    console.log(this.provierUrl)
  }
}
</script>
