<template>  
<div>

  <a class="uk-button uk-button-primary uk-margin" @click="$router.go(-1)"><span uk-icon="arrow-left"></span> Zurück</a>

  <client-only>
  <div uk-grid>

      <div class="uk-child-width-1-3@m uk-grid-small uk-grid-match" uk-grid>
        <div v-for="unterkategorie in kategorie.unterkategories" class="uk-margin">
            <div class="uk-card uk-card-default uk-card-body">
                <div class="uk-card-media-top">
                    <img :src="'http://localhost:1337/' + unterkategorie.image.url" alt="" />
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">{{ unterkategorie.title }} <span class="uk-badge">{{ unterkategorie.Preis }}€</span></h3>
                    <p>{{ unterkategorie.description }}</p>
                </div>
            </div>
        </div>
      </div>
  </div>

  </client-only>
</div>  
</template>

<script>  
import kategorieQuery from '~/apollo/queries/kategorie/kategorie'

export default {  
  data() {
    return {
      kategorie: Object
    }
  },
  apollo: {
    kategorie: {
      prefetch: true,
      query: kategorieQuery,
      variables () {
        return { id: this.$route.params.id }
      }
    }
  }
}
</script>