<template>
  <!-- Main app wrapper start -->
  <div id="app" class="results-wrapper">
    <!-- Search result component starts -->
    <SearchResult 
      v-for="(doctor, index) in doctorsJson" 
      :key="index"
      :docIndex="index"
      :name="doctor.name"
      :specialty="doctor.specialty"
      :portraitImage="doctor.portraitImage"
      :descriptionImages="doctor.descriptionImages"
      :locationDistance="doctor.locationDistance"
      :locationAddress="doctor.locationAddress"
      :categories="doctor.categories"
      @removeEntry="removeEntry"
    />
    <!-- Search result component ends -->

    <!-- When all entries are deleted -->
    <div v-if="this.doctorsList === 0" class="no-entries-available">
      You have deleted all of the entries! Click <a href="javascript:window.location.reload(true)">here</a> to reload the page or add new entry.
    </div>

    <!-- Add new entry button -->
    <button type="button" @click="addEntry()" class="add-entry-button">Eintrag hinzufügen</button>
  </div>
  <!-- Main app wrapper ends -->
</template>

<script>
// Importing components and files
import SearchResult from './components/SearchResult.vue'
import json from './results.json';

export default {
  name: 'App',

  components: {
    SearchResult
  },

  data() {
    return {
      doctorsJson: json.doctors,
      doctorsList: null
    }
  },

  watch: {
    /*
     * Watches the changes in the array and populates the data with the reindexed length
     */
    doctorsJson() {
      this.doctorsList = this.doctorsJson.length
    }
  },

  methods: {
    /*
    * Handles the adding of the new object to the doctors array
    */ 
    addEntry() {
      // Creates the new object
      let newEntry = {
        "id": 3,
        "name": "Dr.Lukas Leitner",
        "specialty": "Augenarzt",
        "portraitImage": "https://st.depositphotos.com/1258191/3252/i/600/depositphotos_32524605-stock-photo-portrait-of-a-handsome-doctor.jpg",
        "descriptionImages": {},
        "locationDistance": "2",
        "locationAddress": "Hietzinger Hauptstrase 2/11, 1130 Wien",
        "categories": [
          "Untersuchung",
          "Beratung",
          "Augenlasern"
        ]
      };
      // Pushes the new object to the array
      this.doctorsJson.push(newEntry);
    },
    /*
    * Handles the removal of the clicked entry
    * Receives the data from the child component
    */
    removeEntry (index) {
      this.$delete(this.doctorsJson, index)
    }
  }
}
</script>

<style>
  /* Imported Google Font */
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400&display=swap');

  * {
    font-family: 'Roboto', sans-serif;
    box-sizing: border-box;
  }

  body {
    background: #e4e5ea;
    margin: 0;
    padding: 0;
  }

  .results-wrapper {
    width: 100%;
    float: left;
    padding: 20px;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    flex-direction: column;
  }

  .add-entry-button {
    width: 100%;
    height: 35px;
    padding: 10px;
    text-align: center;
    color: #ffffff;
    background: #158bd3;
    font-size: 14px;
    border: 0;
    border-radius: 2px;
    transition: all 0.5s;
  }
  .add-entry-button:hover {
    cursor: pointer;
    background: #126FA8;
  }

  .no-entries-available {
    width: 100%;
    float: left;
    text-align: center;
    font-size: 18px;
    margin: 30px 0;
  }
</style>
