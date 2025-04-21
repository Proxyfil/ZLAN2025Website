<script>
import json from '../data/streamers.json'

export default {
  name: 'home',
  components: {

  },
  data() {
    return {
      streamersData: json,
      selected: ""
    }
  },
  methods: {
    lazyload (){
      const blurDivs = document.querySelectorAll('.blur-load');
      blurDivs.forEach((blurDiv) => {
        const img = blurDiv.querySelector('img');

        function loaded() {
          blurDiv.classList.add('loaded');
        }

        if(img.complete) {
          loaded();
          return;
        }
        else{
          img.addEventListener('load', loaded);
        }
      });
    }
  },
  mounted() {
    setTimeout(() => {
      this.lazyload();
    }, 1000);
  }
}
</script>

<template>
  <div class="pt-16 px-8 pb-8">
    <div class="w-full flex justify-center">
      <select v-model="selected" id="select" class="px-4 py-2 w-56 text-center text-white" v-bind:onchange="lazyload">
        <option value="" selected>Statistiques Globales</option>
        <option v-bind:value="'Tous'">
          Tous
        </option>
        <option v-bind:key="option" v-for="option in Object.keys(streamersData).sort()" v-bind:value="option">
          {{ option }}
        </option>
      </select>
    </div>
    <div class="w-full grid grid-cols-6 gap-x-4 gap-y-6 mt-8" v-if="selected == 'Tous'" id="infographics">
      <div class="flex flex-col items-center" v-for="option in Object.keys(streamersData).sort()" v-bind:key="option">
        <a v-bind:href="streamersData[option].linkHD" target="_blank" class="min-h-[300px] blur-load" v-bind:style="{ 'background-image': 'url(' + streamersData[option].lazyload + ')' }"><img class="w-72 min-h-full" v-bind:alt="option" v-bind:src="streamersData[option].img" loading="lazy"></a>
        <p class="text-white mt-2">// {{ option }} //</p>
      </div>
    </div>
    <div class="w-full flex justify-center gap-4 mt-8" v-else-if="selected != ''">
      <div class="flex flex-col items-center">
        <a v-bind:href="streamersData[selected].linkHD" target="_blank" class="min-h-[300px] blur-load" v-bind:style="{ 'background-image': 'url(' + streamersData[selected].lazyload + ')' }"><img class="w-96" v-bind:alt="selected" v-bind:src="streamersData[selected].img" loading="lazy"></a>
        <p class="text-white mt-2">{{ selected }}</p>
      </div>
    </div>
    <div class="w-full grid gird-cols-2 gap-x-4 gap-y-6 gap-4 mt-8" v-else-if="selected == ''" id="infographics_global">
      <div class="flex flex-col items-center">
        <a v-bind:href="'/infographics/one.png'" target="_blank" class="min-h-[300px] blur-load" v-bind:style="{ 'background-image': 'url(' + streamersData['ZERATOR'].lazyload + ')' }"><img class="w-96" v-bind:alt="'infographie globale'" v-bind:src="'/infographics/one.png'" loading="lazy"></a>
      </div>
      <div class="flex flex-col items-center">
        <a v-bind:href="'/infographics/two.png'" target="_blank" class="min-h-[300px] blur-load" v-bind:style="{ 'background-image': 'url(' + streamersData['ZERATOR'].lazyload + ')' }"><img class="w-96" v-bind:alt="'infographie globale #2'" v-bind:src="'/infographics/two.png'" loading="lazy"></a>
      </div>
    </div>
  </div>
</template>

<style scoped>
#select {
  background-color: #57f200;
  border: #57f200 1px solid;
  border-radius: 5px;
  color: #101010;
  font-weight: bold;
}

#select option {
  background-color: #57f200;
  color: #101010;
  font-weight: bold;
}

#infographics div p {
  color: #57f200;
  font-weight: bold;
}

#infographics div img {
  transition: all 0.2s ease-in-out;
}

#infographics div img:hover {
  transform: scale(1.02);
  box-shadow: #57f200 0px 0px 10px;
}

#infographics_global div img {
  transition: all 0.2s ease-in-out;
}

#infographics_global div img:hover {
  transform: scale(1.02);
  box-shadow: #57f200 0px 0px 10px;
}

.blur-load {
  background-size: cover;
  background-position: center;
  filter: blur(3px);
  animation: pulse 2s infinite;
}

.blur-load.loaded {
  animation: none;
  filter: blur(0);
}

.blur-load.loaded img {
  opacity: 1;
}

.blur-load img {
  opacity: 0;
  transition: opacity 0.2s ease-in-out;
}

@keyframes pulse {
  0% {
    filter: blur(3px);
  }
  50% {
    filter: blur(5px);
  }
  100% {
    filter: blur(3px);
  }
}

@media screen and (min-width: 1700px) {
  #infographics_global {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 1700px) {
  #infographics {
    grid-template-columns: repeat(2, 1fr);
  }

  #infographics_global {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 1500px) {
  #infographics {
    grid-template-columns: repeat(2, 1fr);
  }
  #infographics_global {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media screen and (max-width: 1300px) {
  #infographics {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 1000px) {
  #infographics {
    grid-template-columns: repeat(2, 1fr);
  }
  #infographics_global {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 600px) {
  #infographics {
    grid-template-columns: repeat(1, 1fr);
    width: fit-content !important;
  }
  #infographics_global {
    grid-template-columns: repeat(1, 1fr);
  }
  

  #infographics div img {
    max-height: 100% !important;
    width: auto !important;
  }

  #infographics div a {
    width: 80% !important;
  }

  #infographics_global div img {
    max-height: 100% !important;
    width: auto !important;
  }

  #infographics_global div a {
    width: 80% !important;
  }
}

@media screen and (max-width: 500px) {
  #infographics div img {
    max-height: 100% !important;
    width: auto !important;
  }

  #infographics div a {
    width: auto !important;
  }

  #infographics_global div img {
    max-height: 100% !important;
    width: auto !important;
  }

  #infographics_global div a {
    width: auto !important;
  }
}
</style>

