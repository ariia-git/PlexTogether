<template>
  <v-layout row wrap>
    <v-flex xs12 md4 offset-md4>
      <img :src="logo" style="width:100%"/>
      <h2 class="center"> Welcome to Plex Together!</h2>
      <div><span style="font-weight:900">{{ owner }}</span> has invited you to join the room "<span
      style="font-weight:900">{{ room }}</span></div>
      </v-btn>
    </v-flex>
  </v-layout>
</template>
<template>
    <v-layout wrap row ckass="pt-4">
      <v-flex xs12 md8 offset-md2>
        <v-card style="background: rgba(0,0,0,0.3)">
          <h4 class="white--text center-text pa-1"> Welcome to PlexTogether!</h4>
          </div>
          <div class="center-text">
            <h6><span style="font-weight:900">{{ owner }}</span> has invited you to join the room <span
              style="font-weight:900">{{ room }}</span></h6>
          </div>
          <v-layout wrap row class="pa-4">
            <v-flex xs12 md8 offset-md2 class="center-text">       
              <v-btn class="center" style="background-color: #E5A00D" v-on:click.native="letsGo()">Accept Invite</v-btn>     
              </v-flex>      
            </v-layout>
          </div>
          <p style="opacity:0.7" class="center-text">
            PlexTogether is a tool to sync Plex content with your family and friends. For more info click <a target="_blank" href="https://github.com/samcm/plextogether"> here </a>
          </p>
        </v-card>
      </v-flex>      
    </v-layout>
</template>
<script>
  // CSS imports

  export default {
    name: 'join',
    mounted: function () {
      var that = this
      console.log('Hello from join...')
      this.password = this.$route.query.ptpassword
      this.room = this.$route.query.ptroom
      this.server = this.$route.query.ptserver
      this.owner = this.$route.query.owner

      if (this.room && this.server) {
        // Looks like a valid request...
        // Lets setup an auto join and then move the user to /sync
        this.$store.commit('SET_AUTOJOIN', true)
        this.$store.commit('SET_AUTOJOINROOM', this.room)
        this.$store.commit('SET_AUTOJOINPASSWORD', this.password)
        this.$store.commit('SET_AUTOJOINURL', this.server)
      }
    },
    created: function () {
    },
    data () {
      return {
        server: null,
        room: null,
        owner: null
      }
    },
    computed: {
      logo: function () {
        return 'ptweb/logo-small-light.png'
      }
    },
    methods: {
      letsGo () {
        this.$router.push('/sync')
      }
    }

  }
</script>

