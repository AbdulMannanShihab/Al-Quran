<template>
  <div class="min-h-screen bg-gray-200 ">
    <div class="container py-6 px-6 rounded">
        <div class="bg-white p-4 shadow-lg">
            <div class="flex -mx-4">
              <div class="flex-1 px-4">
                  <select @change="getSpaceficSura" class="quran-input" name="" id="">
                    <option value="">Select Sura</option>
                    <option v-for="sura in suras" :value="sura.number">
                      {{ sura.name }}-{{ sura.englishName }}
                    </option>
                  </select>
              </div>
              <div class="flex-1 px-4 py-2 bg-green-400 font-bold text-white">
                <h2>Ayahs : {{ currentSura.numberOfAyahs}} </h2>
              </div>
            </div>
            <div class="text-center p-5 font-bold">
              <p>{{ currentSura.name}}</p>
              <h2>{{ currentSura.englishName}} </h2>
            </div>
            <div class="text-center p-5 mt-1 mb-2">
              <p v-if="currentSura.hasOwnProperty('ayahs')" v-for="ayah in currentSura.ayahs" class="my-2">
                <span> {{ ayah.text }}</span>
              </p>
            </div>
        </div>
       
    </div> 
  </div>
</template>

<script>
  import axios from 'axios'
  export default{
    name: 'App',
    data(){
      return{
        suras: [],
        currentSura: [],
      }
    },

    // lifeCycleFuntion 'mounted'
    mounted() {
      axios.get('https://api.alquran.cloud/v1/surah')
      .then( response => {
       this.suras = response.data.data
      })

      this.querySpacificSura(suraNumber)
    },
    
    // object methods
    methods: {
      getSpaceficSura(e){
        this.querySpacificSura(e.target.value)
      },
      querySpacificSura(suraNumber){
        axios.get('https://api.alquran.cloud/v1/surah/'+ suraNumber)
       
        .then( response => {
          this.currentSura = response.data.data
        })
      }
    }
  }
  

</script>