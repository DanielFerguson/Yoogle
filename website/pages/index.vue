<template>
  <client-only>
    <ais-instant-search :search-client="searchClient" index-name="test_VIDEOS">
      <div class="flex flex-col md:flex-row">
        <!-- Search & Filters -->
        <div
          class="w-full md:w-5/12 lg:w-1/3 p-8 lg:p-16 lg:h-screen text-gray-900"
        >
          <h1 class="text-6xl font-bold">Yoogle</h1>
          <ais-powered-by class="ml-auto" />

          <!-- Search Field -->
          <div class="w-full mt-4 border border-gray-900 rounded-lg">
            <ais-search-box>
              <div slot-scope="{ currentRefinement, isSearchStalled, refine }">
                <input
                  class="appearance-none bg-transparent border-none w-full text-gray-900 placeholder-gray-700 mr-3 py-4 px-6 leading-tight focus:outline-none"
                  v-model="currentRefinement"
                  @input="refine($event.currentTarget.value)"
                  type="search"
                  ref="search"
                  placeholder="Find what you’re looking for"
                  aria-label="search-field"
                />
              </div>
            </ais-search-box>
          </div>

          <!-- Facets -->
          <div class="w-full mt-4 border border-gray-900 rounded-lg p-4 px-6">
            <h2 class="text-4xl font-bold">Facets</h2>

            <!-- Facets - Channels -->
            <div class="my-4">
              <h2 class="text-2xl mb-2 font-thin">Channels</h2>
              <ais-refinement-list
                class="mb-4"
                attribute="channelTitle"
                searchable
              >
                <div
                  slot-scope="{
                    items,
                    isFromSearch,
                    refine,
                    createURL,
                    searchForItems
                  }"
                >
                  <input
                    @input="searchForItems($event.currentTarget.value)"
                    placeholder="Search channels"
                    class="bg-gray-200 py-2 px-3 w-full rounded-lg"
                  />
                  <div v-if="isFromSearch && !items.length">No results.</div>
                  <div class="flex mt-2 overflow-scroll">
                    <div v-for="item in items" :key="item.value">
                      <FacetChip
                        :href="createURL(item)"
                        :active="item.isRefined"
                        @clicked="refine(item.value)"
                      >
                        <ais-highlight attribute="item" :hit="item" />
                      </FacetChip>
                    </div>
                  </div>
                </div>
              </ais-refinement-list>
            </div>

            <!-- Facets - Categories -->
            <div class="my-4">
              <h2 class="text-2xl font-thin">Categories</h2>

              <ais-refinement-list attribute="category">
                <div slot-scope="{ items, isFromSearch, refine, createURL }">
                  <div v-if="isFromSearch && !items.length">No results.</div>
                  <div class="flex mt-2 overflow-scroll">
                    <div v-for="item in items" :key="item.value">
                      <FacetChip
                        :href="createURL(item)"
                        :active="item.isRefined"
                        @clicked="refine(item.value)"
                      >
                        <ais-highlight attribute="item" :hit="item" />
                      </FacetChip>
                    </div>
                  </div>
                </div>
              </ais-refinement-list>
            </div>
          </div>
        </div>

        <!-- Results -->
        <div
          class="w-full md:w-7/12 lg:w-2/3 p-8 lg:p-16 h-screen bg-gradient-to-tr from-purple-700 to-purple-600 max-h-screen overflow-scroll"
        >
          <ais-state-results>
            <div slot-scope="{ state: { query }, results: { hits } }">
              <ais-hits>
                <div
                  slot="item"
                  slot-scope="{ item }"
                  class="w-full border border-white rounded-lg mb-12 max-w-2xl mx-auto"
                >
                  <ResultCard :result="item" :query="query" />
                </div>
              </ais-hits>
            </div>
          </ais-state-results>
        </div>
      </div>
    </ais-instant-search>
  </client-only>
</template>

<script>
// TODO(dan): Intergrate Fathom analytics for website views, searches
// TODO(dan): Intergrate advertising
import algoliasearch from "algoliasearch/lite";

export default {
  data() {
    return {
      searchClient: algoliasearch(
        "2JNWXKECTG",
        "47db2ef808bb7f443b59b4cefafee93c"
      ),
      channels: ["FriendlyJordies", "Sky News", "Dandrews", "Cody Ko"]
    };
  }
};
</script>

<style lang="css">
.transition-default {
  @apply transition duration-75 ease-in-out;
}
</style>
