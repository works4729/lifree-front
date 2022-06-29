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



<!--<template>-->
<!--  <v-container fluid>-->
<!--    <v-card-->
<!--      flat-->
<!--      tile-->
<!--      color="transparent"-->
<!--    >-->
<!--      ...-->
      <!-- 追加 -->
<!--      <v-card-title>-->
<!--        VuetifyカスタムCSSの検証-->
<!--      </v-card-title>-->
<!--      <v-card-text>-->
<!--        ipad（768px）とmobile（426px）で表示・非表示-->
<!--      </v-card-text>-->
<!--      <v-card-text>-->
<!--        <v-card-->
<!--          v-for="(cls, i) in customClass"-->
<!--          :key="`cls-${i}`"-->
<!--          :color="cls.color"-->
<!--          :class="cls.name"-->
<!--        >-->
<!--          <v-card-text>-->
<!--            {{ cls.des }}-->
<!--          </v-card-text>-->
<!--        </v-card>-->
<!--      </v-card-text>-->
      <!-- ここまで -->
<!--    </v-card>-->
<!--  </v-container>-->
<!--</template>-->

<!--<script>-->
<!--export default {-->
<!--  data () {-->
<!--    return {-->
<!--      colors: ['primary', 'info', 'success', 'warning', 'error', 'background'],-->
<!--      customClass: [-->
<!--        { name: 'hidden-ipad-and-down', color: 'error', des: 'ipad未満で隠す' },-->
<!--        { name: 'hidden-ipad-and-up', color: 'info', des: 'ipad以上で隠す' },-->
<!--        { name: 'hidden-mobile-and-down', color: 'success', des: 'mobile未満で隠す' },-->
<!--        { name: 'hidden-mobile-and-up', color: 'warning', des: 'mobile以上で隠す' }-->
<!--      ]-->
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
      <v-card-title>
        Usersテーブルの取得
      </v-card-title>
      <v-card-text>
        <v-simple-table dense>
          <template
            v-if="users.length"
            v-slot:default
          >
            <thead>
              <tr>
                <th
                  v-for="(key, i) in userKeys"
                  :key="`key-${i}`"
                >
                  {{ key }}
                </th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(user, i) in users"
                :key="`user-${i}`"
              >
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>
                <td>{{ dateFormat(user.created_at) }}</td>
              </tr>
            </tbody>
          </template>
          <template v-else>
            ユーザーが存在しません
          </template>
        </v-simple-table>
      </v-card-text>
      <v-card-title>
        Vuetifyの導入（オリジナルカラーの確認）
      </v-card-title>
      <v-card-text>
        <v-btn
          v-for="(color, i) in colors"
          :key="`color-${i}`"
          :color="color"
          class="mr-2"
        >
          {{ color }}
        </v-btn>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  async asyncData ({ $axios }) {
    let users = []
    await $axios.$get('/api/v1/users').then(res => (users = res))
    const userKeys = Object.keys(users[0] || {}) // 追加
    return { users, userKeys }
  },
  // data () 追加
  data () {
    return {
      colors: ['primary', 'info', 'success', 'warning', 'error', 'background']
    }
  },
  computed: {
    dateFormat () {
      return (date) => {
        const dateTimeFormat = new Intl.DateTimeFormat(
          'ja', { dateStyle: 'medium', timeStyle: 'short' }
        )
        return dateTimeFormat.format(new Date(date))
      }
    }
  }
}
</script>