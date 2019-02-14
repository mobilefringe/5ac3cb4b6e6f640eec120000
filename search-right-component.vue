<template>
  <div>
    <!-- without an outer container div this component template will not render -->
    <div id="nav-right" class="nav-right" style>
      <div class="container p-3">
        <label for="searchSite" class="sr-only">Search Beverly Center</label>
        <div class="input-group mb-3">
          <!-- <label for="searchSite" class="hide">Search Site</label> -->
          <!-- <input
            id="searchSite"
            type="text"
            name="search"
            maxlength="35"
            autocomplete="off"
            placeholder="Search Beverly Center"
            class="form-control form-control-lg"
          >-->
          <search-component
            :list="searchList"
            placeholder="Search Beverly Center"
            :suggestion-attribute="suggestionAttribute"
            :keys="keys"
            v-model="search_result"
            @select="onOptionSelect"
            :autocomplete="false"
            :tokenize="true"
            :minMatchCharLength="3"
            class="text-left"
            @updatedResults="updateSearchResults"
          />
          <!-- <a
            href="/search/"
            aria-label="Search Site"
            id="search-site"
            class="btn btn-primary align-self-center"
          >GO</a>-->
        </div>
        <p v-if="storeSearchResultList.length > 0" class="h5 card-title">Stores</p>
        <ul
          role="navigation"
          id="search-results"
          class="list-unstyled pl-4"
          v-if="storeSearchResultList.length > 0"
        >
          <li v-for="result in storeSearchResultList" class="py-1" :key="result.id">
            <nuxt-link
              v-if="result.store_front_url_abs"
              class="result_link hvr-icon-forward"
              :to="{ name: 'stores'}"
            >{{result.name}}</nuxt-link>
          </li>
        </ul>
        <p v-if="promoSearchResultList.length > 0" class="h5 card-title">Promotions</p>
        <ul
          role="navigation"
          id="search-results"
          class="list-unstyled pl-4"
          v-if="promoSearchResultList.length > 0"
        >
          <li v-for="result in promoSearchResultList" class="py-1" :key="result.id">
            <nuxt-link
              v-if="result.promo_image_url_abs"
              class="result_link hvr-icon-forward"
              :to="{ name: 'promotions'}"
            >{{result.name}}</nuxt-link>
          </li>
        </ul>
        <p v-if="eventSearchResultList.length > 0" class="h5 card-title">Events</p>
        <ul
          role="navigation"
          id="search-results"
          class="list-unstyled pl-4"
          v-if="eventSearchResultList.length > 0"
        >
          <li v-for="result in eventSearchResultList" class="py-1" :key="result.id">
            <nuxt-link
              v-if="result.event_image_url_abs"
              class="result_link hvr-icon-forward"
              :to="{ name: 'events'}"
            >{{result.name}}</nuxt-link>
          </li>
        </ul>
        <p v-if="jobSearchResultList.length > 0" class="h5 card-title">Jobs</p>
        <ul
          role="navigation"
          id="search-results"
          class="list-unstyled pl-4"
          v-if="jobSearchResultList.length > 0"
        >
          <li v-for="result in searchResultList" class="py-1" :key="result.id">
            <nuxt-link
              v-if="result.jobable_id"
              class="result_link hvr-icon-forward"
              :to="{ name: 'jobs'}"
            >{{result.name}}</nuxt-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  components: {
    SearchComponent: () => import('~/components/SearchComponent.vue')
  },
  data: function() {
    return {
      search_result: null,
      suggestionAttribute: 'name',
      keys: ['name', 'description', 'tags', 'store.name'],
      searchResultList: [],
      storeSearchResultList: [],
      promoSearchResultList: [],
      eventSearchResultList: [],
      jobSearchResultList: []
    }
  },
  //   async asyncData({ store, params, route }) {
  //     try {
  //       let results = await Promise.all([
  //         store.dispatch('LOAD_SEO', { url: route.fullPath }),
  //         store.dispatch('getData', { resource: 'stores' }),
  //         store.dispatch('getData', { resource: 'categories' })
  //       ])
  //       return { tempSEO: results[1].data.meta_data[0] }
  //     } catch (e) {
  //       console.log(e.message)
  //     }
  //   },
  created() {},
  computed: {
    ...mapGetters([
      'property',
      'timezone',
      'processedStores',
      'processedEvents',
      'processedPromos',
      'processedJobs'
    ]),
    searchList() {
      var events = this.processedEvents
      _.forEach(events, function(value, key) {
        if (_.includes(value.eventable_type, 'Property')) {
          value.is_store = false
        } else {
          value.is_store = true
        }
      })
      var promos = this.processedPromos
      _.forEach(promos, function(value, key) {
        if (_.includes(value.promotionable_type, 'Property')) {
          value.is_store = false
        } else {
          value.is_store = true
        }
      })
      var jobs = this.processedJobs
      _.forEach(jobs, function(value, key) {
        if (_.includes(value.jobable_type, 'Property')) {
          value.is_store = false
        } else {
          value.is_store = true
        }
      })
      var stores = this.processedStores
      _.forEach(stores, function(value, key) {
        value.is_store = true
      })

      var list = _.union(stores, events, promos, jobs)
      return list
    }
  },
  methods: {
    onOptionSelect(option) {
      //   var search_results = option
      //   // change vuex search result to latest result
      //   Promise.all([
      //     this.$store.dispatch('INITIALIZE_SEARCH_RESULT', search_results)
      //   ])
      //   this.$router.push(
      //     this.localePath({
      //       name: 'search-results',
      //       //   params: { searchResults: this.searchResultList },
      //       query: { searchQuery: this.search_result }
      //     })
      //   )
      //   this.$nextTick(function() {
      //     this.search_result = ''
      //   })
    },
    updateSearchResults(results) {
      this.searchResultList = results
      this.storeSearchResultList = _.filter(results, function(o) {
        return o.store_front_url_abs
      })
      this.promoSearchResultList = _.filter(results, function(o) {
        return o.promotionable_type
      })
      this.eventSearchResultList = _.filter(results, function(o) {
        return o.eventable_type
      })
      this.jobSearchResultList = _.filter(results, function(o) {
        return o.jobable_type
      })
      console.log('results', results)
    }
  }
}
</script>
