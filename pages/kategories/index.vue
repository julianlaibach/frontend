<template>  
  <div>

      <form class="uk-search uk-search-large uk-align-center uk-margin">
          <span uk-search-icon></span>
          <input class="uk-search-input" v-model="query" type="search" placeholder="Suchen...">
      </form>


      <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@m uk-margin" v-for="kategorie in filteredList" v-bind:key="kategorie" uk-grid>
          <div class="uk-card-media-left uk-cover-container">
              <img :src="'http://localhost:1337/' + kategorie.image.url" alt="" uk-cover>
              <canvas width="600" height="400"></canvas>
          </div>
          <div>
              <div class="uk-card-body">
                  <h3 class="uk-card-title">{{ kategorie.title }}</h3>
                  <p>{{ kategorie.description }}</p>

                  <router-link :to="{ name: 'kategories-id', params: { id: kategorie.id }}" tag="a" class="uk-button uk-button-primary">Preise Anzeigen
                  </router-link>
              </div>
          </div>
      </div>


      <div class="uk-container uk-container-center uk-text-center" v-if="filteredList.length == 0">
       <img src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800">
       <p>Nichts gefunden</p>
     </div>

  </div>

</template>

<script>  
import kategoriesQuery from '~/apollo/queries/kategorie/kategories'

export default {  
  data() {
    return {
      kategories: [],
      query: ''
    }
  },
  apollo: {
    kategories: {
      prefetch: true,
      query: kategoriesQuery
    }
  },
  computed: {
    filteredList() {
      return this.kategories.filter(kategorie => {
        return kategorie.title.toLowerCase().includes(this.query.toLowerCase())
      })
    },
  }
}
</script>  