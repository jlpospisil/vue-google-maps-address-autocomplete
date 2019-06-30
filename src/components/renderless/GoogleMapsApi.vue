<script>
import GoogleMapsApiLoader from 'google-maps-api-loader';

export default {
  name: 'GoogleMapsApi',
  props: {
    apiKey: {
      required: true,
      type: String,
    },
    libraries: {
      required: true,
      type: Array,
    },
  },
  render: () => null,
  async mounted() {
    const { apiKey, libraries } = this;
    const google = await GoogleMapsApiLoader({
      apiKey,
      libraries,
    });
    this.$emit('loaded', google);
  },
};
</script>

<style lang="scss" scoped>
</style>
