<template>
  <v-ons-page @show="loadUserData">
    <custom-toolbar backLabel="Retour"></custom-toolbar>
    <div class="content">
      <v-ons-list>
        <v-ons-list-title>{{ $t('administratorRecords') }}</v-ons-list-title>
        <v-ons-list-item>
          <div class="center">{{ $t('identificationRecords') }}</div>
          <div class="right">
            <v-ons-switch v-model="identCheck" @change="setIdentificationMode"></v-ons-switch>
          </div>
        </v-ons-list-item>
        <v-ons-list-item>
          <div class="center">{{ $t('showOSMData') }}</div>
          <div class="right">
            <v-ons-switch v-model="showOSM"></v-ons-switch>
          </div>
        </v-ons-list-item>

        <v-ons-list-item>
          <div class="center">{{ $t('allowOSMModif') }}</div>
          <div class="right">
            <v-ons-switch v-model="osmUpdates"></v-ons-switch>
          </div>
        </v-ons-list-item>

        <v-ons-list-item>
          <div class="center">{{ $t('anonymousMode') }}</div>
          <div class="right">
            <v-ons-switch v-model="$store.state.user.isAnon"></v-ons-switch>
          </div>
        </v-ons-list-item>
        <v-ons-list-item>
          <div class="center">{{ $t('deletionMode') }}</div>
          <div class="right">
            <v-ons-switch v-model="$store.state.user.isGod"></v-ons-switch>
          </div>
        </v-ons-list-item>

        <v-ons-list-item>
          <div class="center">{{ $t('expertIdentificationVerificationMode') }}</div>
          <div class="right">
            <v-ons-switch v-model="identificationMode"></v-ons-switch>
          </div>
        </v-ons-list-item>
        <v-ons-list-item>
          <div class="center">{{ $t('recordVerificationMode') }}</div>
          <div class="right">
            <v-ons-switch v-model="verificationMode"></v-ons-switch>
          </div>
        </v-ons-list-item>

        <v-ons-list-item>
          <div class="center">{{ $t('gamificationMode') }}</div>
          <div class="right">
            <v-ons-switch v-model="gamificationMode"></v-ons-switch>
          </div>
        </v-ons-list-item>
        <v-ons-list-item>
          <div class="center">{{ $t('resetSession') }}</div>
          <div class="right">
            <v-ons-button @click="resetSession">Reset</v-ons-button>
          </div>
        </v-ons-list-item>

        <v-ons-list-item v-for="score in scores">
          <div class="center">{{ $t('addButton') }} {{score.displayName}}</div>
          <div class="right">
            <v-ons-button @click="addPoints(score)">{{ $t('addButton') }}</v-ons-button>
          </div>
        </v-ons-list-item>

        <v-ons-list-item>
          <div class="center">{{ $t('upload') }}</div>
          <div class="right">
            <file-upload
              accept=".json"
              class="upload"
              url="/api/uploadMission"
              :thumb-url="thumbUrl"
              @error="error"
              @success="success"
            ></file-upload>
          </div>
        </v-ons-list-item>
        <v-ons-list-item>
          <div class="center">{{ $t('restoreMission') }}</div>
          <div class="right">
            <v-ons-button @click="restoreMission">{{ $t('restore') }}</v-ons-button>
          </div>
        </v-ons-list-item>

      </v-ons-list>
      <v-ons-list></v-ons-list>
      <v-ons-list>
        <v-ons-list-title>{{ $t('usersConnected') }}</v-ons-list-title>
        <v-ons-list-item v-for="(user,index) in userList" v-bind:key="index">
          <div class="center">{{user.info.name}}</div>
        </v-ons-list-item>
      </v-ons-list>
      <v-ons-list
        v-for="(verifications,index) in verificationsByUser"
        v-bind:key="index+'verifications'"
      >
        <v-ons-list-item expandable>
          <v-ons-list-title>{{ $t('VerificationDoneBy') }} {{verifications.user}}</v-ons-list-title>

          <v-ons-list class="expandable-content">
            <v-ons-list-item
              style="display:block;"
              modifier="longdivider"
              v-for="(verif,index) in verifications.data"
              v-bind:key="index+'verifs'"
            >
              <div class="center">
                <b>{{ $t('originRecord') }}</b>
                {{verif.specie}}
                <v-ons-button @click="visualizeReleve(verif)" style="margin-left:40px;">Voir</v-ons-button>
              </div>
              <div class="left" style="display:block">
                <span>
                  <b>{{ $t('userAction') }}</b>
                </span>
                <span v-if="verif.validated">{{ $t('recordValidation') }}</span>
                <span v-if="!verif.validated">{{ $t('recordModification') }} {{verif.userSpecie}}</span>
              </div>
            </v-ons-list-item>
          </v-ons-list>
        </v-ons-list-item>
      </v-ons-list>
      <v-ons-list
        v-for="(identification,index) in identificationByUser"
        v-bind:key="index+'identification'"
      >
        <v-ons-list-item expandable>
          <v-ons-list-title>{{ $t('identificationDoneBy') }}  {{identification.user}}</v-ons-list-title>

          <v-ons-list class="expandable-content">
            <v-ons-list-item
              style="display:block;"
              modifier="longdivider"
              v-for="(ident,index) in identification.data"
              v-bind:key="index+'ident'"
            >
              <div class="center">
                <b>{{ $t('originRecord') }}</b>
                {{ident.specie}} 
                <v-ons-button @click="visualizeReleve(ident)" style="margin-left:40px;">Voir</v-ons-button>
              </div>
              <div class="left" style="display:block">
                <span>
                  <b>{{ $t('userRecord') }} {{ident.userSpecie}}</b>
                </span>
              </div>
            </v-ons-list-item>
          </v-ons-list>
        </v-ons-list-item>
      </v-ons-list>
    </div>
  </v-ons-page>
</template>
<style>
.upload {
    height: 42px;
    width: 69px;
    border-radius: 3px;
    overflow: hidden;}
</style>

<script>
export default {
  data() {
    return {
      identCheck: this.$store.state.releve.identificationMode,
      verifCheck: this.$store.state.releve.verificationMode,
      isAnon: this.$store.state.user.isAnon,
      verificationsByUser: [],
      identificationByUser: []
    };
  },
  computed: {
    userList() {
      return this.$store.state.users.userList;
    },
    scores() {
      return this.$store.state.user.scores;
    },
    gamificationMode:{
      get(){
        return this.$store.state.user.gamificationMode
      },
      set(val){
        this.$store.commit("user/setGamificationMode", val);

      }
    },
    identificationMode: {
      get() {
        return this.$store.state.commonData.identification;
      },
      set(val) {
        this.$store.commit("commonData/setIdentificationMode", val);
      }
    },
    showOSM:{
      get(){
                return this.$store.state.commonData.showOSM;

      },
      set(val){
                this.$store.commit("commonData/showOSM", val);

      }
    },
    osmUpdates: {
      get() {
        return this.$store.state.commonData.osmUpdates;
      },
      set(val) {
        this.$store.commit("commonData/setOsmUpdates", val);
      }
    },

    verificationMode: {
      get() {
        return this.$store.state.commonData.verification;
      },
      set(val) {
        this.$store.commit("commonData/setVerificationMode", val);
      }
    }
  },
  methods: {
    success() {
      //this.resetSession()
    },
    restoreMission(){
      axios.post('/api/restoreMission')
    }
    ,
    error() {
      this.$toasted.show(this.$t('invalidJSON'), {
        theme: "bubble",
        position: "top-center",
        duration: 5000
      });
    },
    thumbUrl() {
      return "";
    },
    addPoints(score) {
      this.$ons.notification
        .prompt("Number of points", {
          inputType: "number",
          title: "Add " + score.displayName,
          defaultValue: 0
        })
        .then(
          function(points) {
            if (points) {
              this.$store.commit("user/addPoints", {
                name: score.name,
                history: {
                  text: "via admin",
                  points: parseInt(points)
                }
              });
            }
          }.bind(this)
        );
    },

    resetSession() {
      axios.post("/api/resetBackup").then(
        function(response) {
          if (response.data.success) {
            window.location.reload();
          }
        }.bind(this)
      );
    },
    visualizeReleve(releve) {
      this.$store.commit("navigator/pop");
      this.$store.commit("tabbar/set", 0);
      this.$root.$emit("changeCenter", releve.coordinates);
    },

    loadUserData() {
      axios.get("/api/identification").then(
        function(response) {
          this.identificationByUser = this.formatResult(response.data);
        }.bind(this)
      );
    },
    formatResult(data) {
      let verifUsers = this.getUserList(data);
      let verifArray = [];
      for (let user of verifUsers) {
        let arrayByUser = data.filter(val => val.username == user);
        verifArray.push({ user: user, data: arrayByUser });
      }
      return verifArray;
    },
    getUserList(array) {
      return [...new Set(array.map(x => x.username))];
    },
    setIdentificationMode(event) {
      this.$store.commit("releve/setIdentificationMode", event.value);
      if (!event.value) return;

      this.$store.commit("commonData/setIdentificationMode", true);
    }
  }
};
</script>
