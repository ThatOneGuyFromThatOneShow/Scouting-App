<template>
  <div
    v-if="loggedin"
    class="grid"
  >
    <div class="location-centered-small done-button-container">
      <h3
        @click="goBack()"
        class="background-box background-box-hover content-centered"
      >Back</h3>
    </div>

    <h1 class="location-span background-box content-centered">Analytics</h1>

    <div class="location-right-large">
      <div
        id="analytics-sorting-options"
        class="background-box content-centered"
      >
        <div>
          <h3>Analytics type</h3>
          <div class="background-box-input">
            <select v-model="analyticsType">
              <option
                disabled
                value=""
              >Select</option>
              <option value="scouting">Scouting</option>
              <option value="comments">Comments</option>
            </select>
          </div>
        </div>

        <div v-show="analyticsType === 'scouting'">
          <h3>Scouting Type</h3>
          <div class="background-box-input">
            <select v-model="scoutingType">
              <option
                disabled
                value=""
              >Select</option>
              <option value="match">Match Scouting</option>
              <option value="pit">Pit Scouting</option>
            </select>
          </div>
        </div>

        <div v-show="scoutingType !== ''">
          <h3>Scouting Question</h3>
          <div class="background-box-input">
            <select v-model="scoutingQuestion">
              <option
                disabled
                value=""
              >Select</option>
              <option value="d">v-for</option>
              <option value="dfadfa">Sort by Comments</option>
            </select>
          </div>
        </div>

        <div v-show="analyticsType === 'comments' || scoutingQuestion !== ''">
          <h3>Sorting Method</h3>
          <div class="
          background-box-input">
            <select v-model="sortingMethod">
              <option value="">Average</option>
              <option value="">Highest</option>
              <option value="">Lowest</option>
            </select>
          </div>
        </div>
      </div>
    </div>

  </div>
  <Error v-else>You must be logged in to view this page!</Error>
</template>

<script>
import Error from "./Error.vue";

export default {
  name: "MenuAnalytics",
  components: {
    Error
  },
  props: {
    localdb: Object,
    remotedb: Object,
    sync_change: Object,
    user: Object,
    reloadSync: Function
  },
  data() {
    return {
      analyticsType: "",
      scoutingType: "",
      scoutingQuestion: "",
      sortingMethod: "",
      teams: [],
      loggedin: true
    };
  },
  methods: {
    goBack() {
      this.$router.push("/");
    }
  },
  watch: {
    user: {
      handler: function(newValue) {
        if (
          newValue.role === "_admin" ||
          newValue.role === "edit" ||
          newValue.role === "view"
        ) {
          this.loggedin = true;
        } else {
          this.loggedin = false;
        }
      },
      deep: true
    }
  }
};
</script>

<style>
#analytics-sorting-options * {
  --box-color: var(--background-color);
}

@media (min-width: 1200px) {
  #analytics-sorting-options {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>

