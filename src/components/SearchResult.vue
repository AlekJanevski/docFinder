<template>
  <div class="search-result-wrapper">
    <!-- Top section starts -->
    <div class="search-result-content-top">
      <!-- Doctor's image -->
      <div class="content-doc-image" :style="{ 'background-image': 'url(' + portraitImage + ')' }">
        <!-- Background image added of the portrait -->
      </div>
      <!-- Info section starts -->
      <div class="content-doc-info">
        <!-- Doctor's name and surname -->
        <span class="content-doc-name">
          {{ name }}
        </span>
        <!-- Doctor's specialty -->
        <span class="content-doc-specialty">
          {{ specialty }}
        </span>
        <!-- Patient images -->
        <div class="content-pat-images">
          <!-- If there are images available-->
          <div v-if="areDescriptionImagesAvailable">
            <img v-for="img in descriptionImages" :key="img.index" :src="img" alt="doc-content">
          </div>
          <!-- If there are no images available-->
          <div v-else class="content-empty">
            No images available
          </div>
        </div>
        <!-- Doctor's location -->
        <div class="content-doc-location">
          <!-- Distance in km -->
          <span class="location-distance">
            <!-- Location icon -->
            <svg role="img" xmlns="http://www.w3.org/2000/svg" width="13px" height="13px" viewBox="0 0 24 24" aria-labelledby="locationIconTitle" stroke="#777777" stroke-width="2" stroke-linecap="square" stroke-linejoin="miter" fill="none" color="#2329D6"> <title id="locationIconTitle">Location</title> <path d="M12,21 C16,16.8 18,12.8 18,9 C18,5.6862915 15.3137085,3 12,3 C8.6862915,3 6,5.6862915 6,9 C6,12.8 8,16.8 12,21 Z"/> <circle cx="12" cy="9" r="1"/></svg>
            {{ locationDistance }} km
          </span>
          <!-- Address of the location -->
          <span class="location-address">
            {{ locationAddress }}
          </span>
        </div>
      </div>
      <!-- Info section ends -->
    </div>
    <!-- Top section ends -->

    <!-- Bottom section starts -->
    <div class="search-result-content-bottom">
      <!-- Specialty tags -->
      <div class="content-tags-wrapper">
        <!-- If there are categories -->
        <div v-if="areCategoriesAvailable">
          <span v-for="(category, index) in categories" 
                :key="index" 
                class="content-tag"
          >
            {{ category }}
          </span>
        </div>
        <!-- If there are no categories -->
        <div v-else  class="content-empty">
          No categories available
        </div>
      </div>
      <!-- Delete button -->
      <div class="content-button">
        <button type="button" @click="removeDoctor(docIndex)">Eintrag löschen</button>
      </div>
    </div>
    <!-- Bottom section ends -->
  </div>
</template>

<script>
export default {
  name: 'SearchResult',

  props: {
    docIndex: Number,
    name: String,
    specialty: String,
    portraitImage: String,
    descriptionImages: Object,
    locationDistance: String,
    locationAddress: String,
    categories: Array
  },

  computed: {
    /**
     * Checks if description images are available
     * returns @boolean
     */
    areDescriptionImagesAvailable() {
      return Object.keys(this.descriptionImages).length === 0 ? false : true
    },
    /**
     * Checks if there are categories added
     * returns @boolean
     */
    areCategoriesAvailable() {
      return this.categories.length === 0 ? false : true
    }
  },

  methods: {
    /**
     * Handles the removal of the entry
     * @emits event to the parent component
     */
    removeDoctor(docIndex) {
      this.$emit('removeEntry', docIndex);
    },
  }
}
</script>

<style scoped>
  .search-result-wrapper {
    width: 100%;
    float: left;
    padding: 20px;
    margin-bottom: 20px;
    background: #ffffff;
  }
  .search-result-wrapper:last-child {
    margin-bottom: 0;
  }
  .search-result-content-top,
  .search-result-content-bottom {
    width: 100%;
    float: left;
  }
  .search-result-content-top {
    margin-bottom: 30px;
  }

  .content-doc-image {
    width: 15%;
    height: 160px;
    float: left;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
  }

  .content-doc-info {
    width: 85%;
    float: left;
    padding-left: 20px;
    text-align: left;
  }
  .content-doc-name {
    display: block;
    font-size: 16px;
    margin-bottom: 5px;
  }
  .content-doc-specialty {
    display: block;
    font-size: 12px;
    color: #6C6C6C;
    text-align: left;
    margin-bottom: 20px;
  }
  .content-pat-images {
    width: 100%;
    float: left;
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }
  .content-empty {
    font-size: 12px;
  }
  .content-pat-images img {
    width: 150px;
    height: 100px;
    margin-right: 5px;
  }
  .content-pat-images img:last-of-type {
    margin-right: 0;
  }
  .content-doc-location {
    width: 100%;
    float: left;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  .location-distance {
    display: flex;
    align-items: center;
    font-size: 12px;
    color: #6C6C6C;
    margin-right: 20px;
  }
  .location-address {
    display: inline-block;
    font-size: 12px;
    color: #6C6C6C;
  }

  .search-result-content-bottom {
    width: 100%;
    float: left;
  }
  .content-tags-wrapper {
    width: 100%;
    float: left;
    display: flex;
    margin-bottom: 10px;
  }
  .content-tag {
    width: auto;
    padding: 5px;
    border: 1px solid #CCCCCC;
    border-radius: 2px;
    color: #158bd3;
    margin-right: 5px;
    font-size: 12px;
    cursor: pointer;
  }
  .content-tag:last-of-type {
    margin-right: 0;
  }
  .content-button {
    width: 100%;
    float: left;
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }
  .content-button button {
    width: 200px;
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
  .content-button button:hover {
    cursor: pointer;
    background: #126FA8;
  }
</style>
