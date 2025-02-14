<template>
  <div class="container">
    <h1 class="text-lg font-bold">OAuth Request</h1>
    <button @click="getRequestToken" class="px-4 py-2 bg-blue-500 text-white rounded-lg">
      Pobierz Token
    </button>

    <div v-if="token" class="mt-4">
      <p class="text-green-600">Token żądania:</p>
      <pre>{{ token }}</pre>
    </div>

    <div v-if="error" class="mt-4">
      <p class="text-red-600">Błąd:</p>
      <pre>{{ error }}</pre>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import axios from 'axios'
import oauthSignature from 'oauth-signature'
import qs from 'qs'

export default defineComponent({
  name: 'OAuthRequest',
  data() {
    return {
      consumerKey: 'CONSUMER_KEY',
      consumerSecret: 'CONSUMER_SECRET',
      requestTokenUrl: 'https://apps.usos.pw.edu.pl/services/oauth/request_token',
      token: null as string | null,
      error: null as string | null,
    }
  },
  methods: {
    async getRequestToken(): Promise<void> {
      const oauthParams = {
        oauth_consumer_key: this.consumerKey,
        oauth_nonce: Math.random().toString(36).substring(2),
        oauth_signature_method: 'HMAC-SHA1',
        oauth_timestamp: Math.floor(Date.now() / 1000),
        oauth_version: '1.0',
      }

      try {
        const signature = oauthSignature.generate(
          'POST',
          this.requestTokenUrl,
          oauthParams,
          this.consumerSecret,
        )

        oauthParams.oauth_signature = signature

        const response = await axios.post(this.requestTokenUrl, qs.stringify(oauthParams), {
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
          },
        })

        console.log('Odpowiedź serwera:', response.data)
        this.token = response.data
      } catch (err: any) {
        console.error('Błąd podczas żądania tokenu:', err.response?.data || err.message)
        this.error = err.response?.data || 'Błąd połączenia.'
      }
    },
  },
})
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}
</style>
