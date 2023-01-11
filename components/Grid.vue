<template>
    <div class="container mx-auto grid sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 pt-6 gap-8 game-items">
        <div v-for="game in games" :key="game.id" class="rounded-lg game-item">
            <nuxt-link :to="`/games/game/${game.slug}`">
                <div class="max-w-sm rounded overflow-hidden shadow-lg game-image" :style="'background-image: url('+game.background_image+')'">
                <div class="game-item-meta">
                    <div class="px-6 py-4">
                        <div class="font-bold text-xl mb-2 text-white">{{game.name}}</div>
                            <p class="text-white text-base">
                                {{game.released}}
                            </p>
                        </div>
                        <div class="px-6 pt-4 pb-2">
                            <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#photography</span>
                            <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#travel</span>
                            <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#winter</span>
                        </div>
                    </div>
                </div>
            </nuxt-link>
        </div>
    </div>
</template>

<script lang="ts" scoped>
import Vue from 'vue'

export default Vue.extend({
  name: 'Grid',
  data() {
    return {
    }
  },
  props: {
    games: Array
  },
})

</script>

<style>

.game-item:hover .game-item-meta:before{
    height: 150px;
}

.game-item:hover .game-item-meta:before{
    
}

.game-item-meta{
    position: relative;
    background-color: #1e2f4a;
}

.game-item-meta:before{
    content: '';
    position: absolute;
    top: 5px;
    translate: 0px -100%;
    left: 0;
    width: 100%;
    height: 100px;
    background: linear-gradient(0deg, rgba(30,47,74,1) 5%, rgba(30,47,74,0) 100%);
    transition: all 0.3s ease-in-out;
}

.game-image{
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    padding-top: 300px;
}


</style>
