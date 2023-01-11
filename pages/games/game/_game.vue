<template>
  <div>
    <Header />
    <main>
      <section class="not-hidden section-game-image z-[-1] relative mb-[-40vh] h-screen" :style="'background-image: url('+game.background_image+')'">
      </section>
      <section class="container mx-auto not-hidden">
        <h1 class="mt-[100px] text-5xl text-white">{{ game.name }}</h1>
      </section>
      <section class="h-screen container mx-auto pt-5">
          <p></p>
          <div class="grid sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-2 xl:grid-cols-2 pt-6 gap-8">
            <div>
                <h2 class="text-2xl pb-2 text-white">Description:</h2>
                <p class="text-base text-white">{{ game.description_raw }}</p>
            </div>
            <div>
                <div class="lg:max-w-[50%] lg:mr-0 lg:ml-auto">
                    <h2 class="text-2xl pb-2 text-white">Developers:</h2>
                    <div class="flex flex-wrap gap-2">
                        <nuxt-link to="#" class="p-2 px-4 bg-[#23395d] hover:bg-[#1e2f4a] rounded-full text-white" v-for="dev in game.developers" :key="dev.id">{{ dev.name }}</nuxt-link>
                    </div>
                </div>
                <div class="lg:max-w-[50%] lg:mr-0 lg:ml-auto pt-5">
                    <h2 class="text-2xl pb-2 text-white">Plataforms:</h2>
                    <div class="flex flex-wrap gap-2">
                        <nuxt-link to="#" class="p-2 px-4 bg-[#23395d] hover:bg-[#1e2f4a] rounded-full text-white" v-for="platform in game.platforms" :key="platform.id">{{ platform.platform.name }}</nuxt-link>
                    </div>
                </div>
            </div>
        </div>
      </section>
      
    </main>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import { gsap } from "gsap/dist/gsap";
import { ScrollTrigger } from "gsap/dist/ScrollTrigger";

export default Vue.extend({
    name: 'Game',
    data() {
        return {
            game: {}
        }
    },
    beforeMount() {
        
        fetch('https://api.rawg.io/api/games/'+this.$route.params.game+'?key='+process.env.apiKey+'&page_size=5')
            .then(response => response.json())
            .then(data => {
            
                var game = data;
                this.game = game;
                console.log(game);
                
            })

    },
    mounted() {
        gsap.registerPlugin(ScrollTrigger);
        
        var tl = gsap.timeline();
        tl.to(".section-game-image", {
            scrollTrigger: {
                trigger: ".section-game-image",
                start: "top-=60 top",
                end: "bottom-=40vh-=50% top",
                scrub: true,
                markers: false
            },
            opacity: 0,
            y: '-60vh',
            duration: 1
        });

        tl.to("main section:not(.not-hidden)", {
            scrollTrigger: {
                trigger: ".section-game-image",
                start: "top+=50% center",
                end: "bottom center",
                scrub: true,
                markers: false
            },
            opacity: 1,
            duration: 1
        });

    },
    beforeDestroy() {
        ScrollTrigger.getAll().forEach((trigger) => {
            trigger.kill()
        });
    }
    
    
})

</script>

<style>

.section-game-image{
    background-position: 50% 0%;
    background-repeat: no-repeat;
    background-size: cover;
    width: 100%;
    background-color: #000;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
    opacity: 1;

    border-radius: 0px 0px 20px 20px;
}

.section-game-image:before{
    content: '';
    position: absolute;
    bottom: -5px;
    left: 0;
    width: 100%;
    height: 50vh;
    color:152238;
    background: linear-gradient(0deg, rgba(12,34,56,1) 10%, rgba(12,34,56,0) 100%);
}

.rating-text{
  font-weight: bold;
  font-size: 1.9em;
  border: 1px solid #cfcfcf;
  padding-left: 10px;
  padding-right: 10px;
  border-radius: 5px;
  color: #999;
  background: #fff;
}

section:not(.not-hidden){
    opacity: 0;
}

</style>

