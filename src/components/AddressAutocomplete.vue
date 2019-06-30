<template>
  <div class="address-autocomplete">
    <google-maps-api-loader
      :apiKey="googleMapsApiKey"
      :libraries="['places']"
      @loaded="googleMapsLoaded"
    />

    <input
      type="text"
      ref="autocompleteInput"
      autofocus
    />

    <vue-json-pretty
      class="selected-address"
      :data="{ address: selectedAddress }"
      v-if="selectedAddress"
    />
  </div>
</template>

<script>
import VueJsonPretty from 'vue-json-pretty';
import GoogleMapsApiLoader from './renderless/GoogleMapsApiLoader.vue';

export default {
  name: 'AddressAutocomplete',
  components: {
    GoogleMapsApiLoader,
    VueJsonPretty,
  },
  data() {
    return {
      autocomplete: null,
      selectedAddress: null,
    };
  },
  computed: {
    googleMapsApiKey() {
      return process.env.VUE_APP_GOOGLE_MAPS_API_KEY;
    },
  },
  methods: {
    googleMapsLoaded(google) {
      if (google) {
        const { addressSelected } = this;
        const { autocompleteInput } = this.$refs;
        this.autocomplete = new google.maps.places.Autocomplete(autocompleteInput, { types: ['geocode'] });
        this.autocomplete.addListener('place_changed', addressSelected);
      }
    },
    addressSelected() {
      const { autocomplete } = this;
      const { address_components: address } = autocomplete.getPlace();
      this.selectedAddress = address;
    },
  },
};
</script>

<style lang="scss" scoped>
$width: 500px;

.address-autocomplete {
  text-align: center;

  input {
    width: $width;
    padding: 10px;
    margin-bottom: 15px;
  }

  .selected-address {
    width: $width;
    height: 400px;
    overflow-y: auto;
    padding: 10px;
    background-color: #f8f8f8;
    text-align: left;
    border: 1px solid #dedede;
    margin: 0 auto;
  }
}
</style>
