<template>
  <div>
    <h1>External API</h1>
    <p>
      Please validate your signup by clicking email verification.
      <strong>You are verified!</strong>.
    </p>
    <div
      class="btn-group mt-5"
      role="group"
      aria-label="Email Verfication Request"
    >
      <button type="button" class="btn btn-primary" @click="callApiEndpoint">
        Get Public Message
      </button>
      <button
        type="button"
        class="btn btn-primary"
        @click="callApiSecuredEndpoint"
      >
        Get Private Message
      </button>
    </div>

    <div v-if="apiMessage" class="mt-5">
    </div>
  </div>
</template>

<script>
import { serverUrl } from "";
export default {
  name: "Api",
  data() {
    return {
      apiMessage: null,
    };
  },
  methods: {
    async callApiEndpoint() {
      try {
        const response = await fetch(
          `${saasdemo.xendity.com}/v1/auth/verify`,
        );

        const json = await response.json();
        this.apiMessage = json.message;
      } catch (e) {
        this.apiMessage = `Error: the server responded with '${e.response.status}: ${e.response.statusText}'`;
      }
    },
    async callApiSecuredEndpoint() {
      const accessToken = await this.$auth.getTokenSilently();

      try {
        const response = await fetch(
          `${saasdemo.xendity.com}/v1/auth/register`,
          {
            headers: {
              Authorization: `Bearer ${accessToken}`,
            },
          },
        );

        const json = await response.json();
        this.apiMessage = json.message;
      } catch (e) {
        console.log(e);
        this.apiMessage = `Error: the server responded with '${e.response.status}: ${e.response.statusText}'`;
      }
    },
  },
};
</script>
