<template >
  <div id="app" >
    <div id="filter">
      <input type="radio" name="radAnswer" value="allt" id="filter1" checked>Allt
      <input v-model="petrol.company" v-bind="SortedFilteredStations " type="radio" name="radAnswer" value="Atlantsolía"  id="filter2">Atlantsolía
      <input v-model="petrol.company" type="radio" name="radAnswer" value="Costco Iceland" id="filter3">Costco Iceland
      <input v-model="petrol.company" type="radio" name="radAnswer" value="Dælan" id="filter4">Dælan
      <input v-model="petrol.company" type="radio" name="radAnswer" value="N1" id="filter5">N1
      <input v-model="petrol.company" type="radio" name="radAnswer" value="Olís" id="filter6">Olís
      <br>
      <input v-model="petrol.company" type="radio" name="radAnswer" value="Orkan" id="filter7">Orkan
      <input v-model="petrol.company" type="radio" name="radAnswer" value="Orkan X" id="filter8">Orkan X
      <input v-model="petrol.company" type="radio" name="radAnswer" value="ÓB" id="filter9">ÓB
      <input v-model="petrol.company" type="radio" name="radAnswer" value="Skeljungur" id="filter10">Skeljungur
    </div>
    
    <div id="fjoldi">
      Fjöldi stöðva: {{petrol.length}}
    </div>
    
    <div v-for="petrol in SortedFilteredStations" id="kassi">
        <div id="inline1">
          <h2 id="compName"> {{ petrol.company }}</h2>
          <h5 id="bensinPrice">Bensín kostnaður: {{ petrol.bensin95 }}</h5>
          
          
          
        </div>
         <div id="inline1">
          <h4 id="petrName">{{ petrol.name }}</h4>
        <h5 id="dieselPrice" >Díesel kostnaður: {{ petrol.diesel }}</h5>

        
      </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
      petrol: []
    };
  },

  mounted() {
    var self = this;
    axios.get('http://apis.is/petrol')
      .then(function(response){
        self.petrol = response.data.results
          
      })

      .catch(function(errors) {
          console.log(errors)
      })
  },

   computed: {
    SortedFilteredStations(){
      var stations = this.petrol.sort(function(a,b){
        return a.bensin95 - b.bensin95;
      });

      return stations.filter(function(petrol) {
        return petrol.company === petrol.company;



      });
    }
  }
}


</script>

<style >

  body {
    
    max-width: 100%;
    padding-left: 20%;
    padding-right: 20%;
  }

  #filter{
    text-align: center;
  }

  #kassi {
    
    margin-bottom: 1em;
    border: solid grey 2px;
    border-radius: 20px;
  
  }

  #inline1{
    
    display: flex;
    justify-content: space-between;
    padding-left: 10px;
    padding-right: 10px;
    
  }

   #inline2{
  
    display: flex;
    justify-content: space-between;
    padding-right: 10px;
    padding-left: 10px;
  }

h5{
  color: grey;
}

   #kassi:hover h5 {
    color: black;  
  }



</style>