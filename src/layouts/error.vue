<!-- HEALTH:UNKNOWN __page__error -->
<template>
  <div class="__page__error">
    <container>
      <div class="text-center mt-col">
        <h1>{{ code }}</h1>
        <h2>{{ message | uc_first }}</h2>
        <smart-link class="underline" href="/" :external="$route.path === '/'">
          Home page
        </smart-link>
      </div>
    </container>
  </div>
</template>

<script>
const unknown = "Something happened, but we're taking care of it!";

export default {
  props: {
    error: {
      type: Object,
      default: () => ({
        code: "Unknown",
        message: ""
      })
    }
  },
  computed: {
    code() {
      return this.error.statusCode || this.error.code;
    },
    message() {
      return this.error.msg /*|| statusMsg[this.code]*/ || unknown;
    }
  },
  mounted() {
    this.$store.dispatch("pageChanged");
  },
  head() {
    return this.$buildHead({
      title: `${this.code}` || "💐",
      description: this.$options.filters.uc_first(this.message),
      metaImage: { og: undefined, tw: undefined },
      path: this.$route.path
    });
  }
};
</script>

<style lang="sass" scoped>
// .__page__error
</style>
