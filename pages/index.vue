<!--<template>-->
<!--  <div>-->
<!--    index.vue-->
<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--export default {-->
<!--  layout ({ store }) {-->
<!--    return store.state.loggedIn ? 'default' : 'welcome'-->
<!--  }-->
<!--}-->
<!--</script>-->



<!--<template>-->
<!--  <div>-->
<!--    <button-->
<!--      type="button"-->
<!--      name="button"-->
<!--      @click="getMsg"-->
<!--    >-->
<!--      RailsからAPIを取得する-->
<!--    </button>-->
<!--    <div-->
<!--      v-for="(msg, i) in msgs"-->
<!--      :key="i"-->
<!--    >-->
<!--      {{ msg }}-->
<!--    </div>-->
<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--export default {-->
<!--  data () {-->
<!--    return {-->
<!--      msgs: []-->
<!--    }-->
<!--  },-->
<!--  methods: {-->
<!--    getMsg () {-->
<!--      this.$axios.$get('/api/v1/hello')-->
<!--        .then(res => this.msgs.push(res))-->
<!--    }-->
<!--  }-->
<!--}-->
<!--</script>-->



<template>
  <v-container fluid>
    <v-card
      flat
      tile
      color="transparent"
    >
      ...
      <!-- 追加 -->
      <v-card-title>
        VuetifyカスタムCSSの検証
      </v-card-title>
      <v-card-text>
        ipad（768px）とmobile（426px）で表示・非表示
      </v-card-text>
      <v-card-text>
        <v-card
          v-for="(cls, i) in customClass"
          :key="`cls-${i}`"
          :color="cls.color"
          :class="cls.name"
        >
          <v-card-text>
            {{ cls.des }}
          </v-card-text>
        </v-card>
      </v-card-text>
      <!-- ここまで -->
    </v-card>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      colors: ['primary', 'info', 'success', 'warning', 'error', 'background'],
      // 追加
      customClass: [
        { name: 'hidden-ipad-and-down', color: 'error', des: 'ipad未満で隠す' },
        { name: 'hidden-ipad-and-up', color: 'info', des: 'ipad以上で隠す' },
        { name: 'hidden-mobile-and-down', color: 'success', des: 'mobile未満で隠す' },
        { name: 'hidden-mobile-and-up', color: 'warning', des: 'mobile以上で隠す' }
      ]
    }
  }
}
</script>