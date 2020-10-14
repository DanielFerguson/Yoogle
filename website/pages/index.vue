<template>
  <div class="flex flex-col md:flex-row">
    <!-- Search & Filters -->
    <div
      class="w-full md:w-5/12 lg:w-1/3 p-8 lg:p-16 lg:h-screen text-gray-900"
    >
      <h1 class="text-6xl font-bold">Yoogle</h1>

      <!-- Search Field -->
      <div class="w-full mt-4 border border-gray-900 rounded-lg">
        <input
          class="appearance-none bg-transparent border-none w-full text-gray-900 placeholder-gray-700 mr-3 py-4 px-6 leading-tight focus:outline-none"
          type="text"
          placeholder="Find what you’re looking for"
          aria-label="search-field"
        />
      </div>

      <!-- Facets -->
      <div
        class="w-full mt-4 border border-gray-900 rounded-lg shadow p-4 px-6"
      >
        <h2 class="text-4xl font-bold">Facets</h2>

        <!-- Facets - Channels -->
        <div class="mb-4">
          <h2 class="text-2xl font-thin">Categories</h2>

          <div class="flex mt-2 overflow-scroll">
            <FacetChip v-for="category in categories" :key="category">
              {{ category }}
            </FacetChip>
          </div>
        </div>

        <!-- Facets - Channels -->
        <div class="my-4">
          <h2 class="text-2xl font-thin">Channels</h2>

          <div class="flex mt-2 overflow-scroll">
            <FacetChip v-for="channel in channels" :key="channel">
              {{ channel }}
            </FacetChip>
          </div>
        </div>
      </div>
    </div>

    <!-- Results -->
    <div
      class="w-full md:w-7/12 lg:w-2/3 p-8 lg:p-16 h-screen bg-gradient-to-r from-purple-900 to-purple-800 max-h-screen overflow-scroll"
    >
      <!-- TODO(dan): Setup with Algolia InstantSearch ais-hits components -->
      <div v-if="false" class="text-white">
        Try searching for captions!
      </div>
      <div v-else>
        <div
          v-for="i in 10"
          :key="i"
          class="w-full border border-white rounded-lg mb-12 max-w-2xl mx-auto"
        >
          <ResultCard />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// TODO(dan): Intergrate Algolia
// TODO(dan): Intergrate Fathom analytics for website views, searches
// TODO(dan): Intergrate advertising

export default {
  data() {
    return {
      categories: [
        "Comedy",
        "News",
        "Thriller",
        "Informative",
        "Informative",
        "Informative"
      ],
      channels: ["FriendlyJordies", "Sky News", "Dandrews", "Cody Ko"]
    };
  }
};
</script>

<style lang="css" scoped>
.transition-default {
  @apply transition duration-75 ease-in-out;
}
</style>
