<template>
  <a class="btn btn-default btn-block m-t-0 -sidebar-btn"
    :class="{ '-matched-route': amIMatched }"
    v-link="vlinkContent">
    <i :class="icon" class="m-r-5"></i>
    {{ title }}
  </a>
</template>
<script>
export default {
  props: {
    path: { type: String, required: true },
    title: { type: String, required: true },
    icon: { type: String, default: 'fa fa-link' },
    isExact: { type: Boolean, default: false }
  },
  computed: {
    curMatchedPath () {
      return this.$route.matched.slice(-1)[0].handler.fullPath
    },
    amIMatched () {
      return this.path === this.curMatchedPath
    },
    vlinkContent () {
      if (this.amIMatched) return
      return { path: this.path, exact: this.isExact }
    }
  }
}
</script>
<style>
.m-t-0 {
  margin-top: 0 !important;
}
.-matched-route {
  color: #3bafda !important;
}
</style>
