<template>
  <div>
    <google-maps-api
      :apiKey="googleMapsApiKey"
      :libraries="['places']"
      @loaded="googleMapsLoaded"
    />
  </div>
</template>

<script>
import GoogleMapsApi from './renderless/GoogleMapsApi.vue';

export default {
  name: 'AddressAutocomplete',
  components: {
    GoogleMapsApi,
  },
  computed: {
    googleMapsApiKey() {
      return process.env.VUE_APP_GOOGLE_MAPS_API_KEY;
    },
  },
  methods: {
    googleMapsLoaded(google) {
      console.log({ google });
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
