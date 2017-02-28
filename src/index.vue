<template>
  <div id="sidebar">
    <div class="clearfix m-b-10">
      <h1 class="-main-title cursor-pointer" v-link="'/'">
        {{ mainTitle }}
      </h1>
      <span class="-sub-title pull-right m-r-10">
        {{ subTitle }}
      </span>
    </div>
    <template v-for="route in routes">
      <template v-if="route.showInSidebar">
        <div v-if="route.subRoutes">
          <a :href="'#panel'+$index"
            class="btn btn-default btn-block -sidebar-btn"
            data-toggle="collapse" data-parent="#sidebar">
            <i :class="route.icon" class="m-r-5"></i>
            {{ route.title }}
            <span class="caret"></span>
          </a>
          <div :id="'panel'+$index" class="collapse">
            <template v-for="subRoute in route.subRoutes">
              <link class="-sub-route" v-if="subRoute.showInSidebar"
                :path="subRoute.fullPath"
                :title="subRoute.title"
                :icon="subRoute.icon">
              </link>
            </template>
          </div><!-- .collapse -->
        </div><!-- v-if -->
        <link v-else
          :path="route.path"
          :title="route.title"
          :icon="route.icon"
          :is-exact="true">
        </link>
      </template>
    </template>
  </div>
</template>
<script>
import Link from './Link.vue'

export default {
  components: { Link },
  props: {
    mainTitle: String, subTitle: String,
    routes: { type: Object, required: true }
  },
  watch: {
    '$route.path' () {
      this.expand()
    }
  },
  attached () {
    this.expand()

    // only allow one collapse to open at the same time
    const $el = $(this.$el)
    $el.on('show.bs.collapse', 'div.collapse', function () {
      const panelId = this.id
      $el.find('div.collapse').each(function () {
        if (this.id !== panelId) $(this).collapse('hide')
      })
    })
  },
  methods: {
    // if now in a second-level route, open its parent collapse
    expand () {
      $(this.$el)
        .find('a.-matched-route')
        .parents('div.collapse')
        .collapse('show')
    }
  }
}
</script>
<style>
.m-r-5 {
  margin-right: 5px;
}
.m-r-10 {
  margin-right: 10px;
}
.m-b-10 {
  margin-bottom: 10px;
}
.cursor-pointer {
  cursor: pointer;
}
#sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 150px;
  height: 100%;
  background-color: #2e363f;
}
.-main-title {
  color: #3bafda;
  font-size: 26px;
  font-weight: 700;
  text-align: center;
  letter-spacing: .03em;
  text-shadow: 1px 1px 2px #000;
}
.-sub-title {
  color: #717171;
  font-size: 13px;
  text-shadow: 1px 1px 1px #2f2f2f;
}
.-sidebar-btn {
  position: relative;
  padding: 10px 12px;
  text-align: left;
  font-size: 14px;
  color: #a2acae;
  background-color: #24292f;
  border-color: transparent;
  border-radius: 0;
  border-top: 1px solid #37414b;
  border-bottom: 1px solid #111519;
  border-left-width: 0;
  border-right-width: 0;
}
.-sidebar-btn > i {
  width: 20px;
  text-align: center;
}
.-sub-route {
  border: none;
  color: #75767B;
  background-color: #202429;
  padding-left: 20px;
}
.-sub-route:hover {
  color: #fff;
  background-color: #202429;
}
.-sidebar-btn .caret {
  position: absolute;
  top: 50%;
  right: 10px;
  transform: translate(0, -50%);
}
</style>
