<template>
  <div class="page corners padding transp">
    <header>
      <nav class="nav flex-column flex-sm-row">
        <router-link class="flex-sm-fill flex-grow-1 text-sm-left nav-link active" to ="/"><h1>Lumia</h1></router-link>
        <router-link class="text-sm-right nav-link" to="/Contact">Kontakta oss</router-link>
      </nav>
    </header>
    <main>
      <div>
        <input class="flex-sm-fill text-sm-center nav-link" v-model="search" type="text" 
        id="search" placeholder="Type to search" data-change="search">
        <div v-for="(lamp,index) in filteredLamps"
         :key="index">
        
      
        <div class="lamps">
          <div class="product clearfix">
            <img :src="lamp.image">
              
            <div class="content">
              <h2>{{lamp.name}}</h2>
              <p>{{lamp.description}}</p>
              <button data-click="buy" v-on:click="buyLamp(lamp)">Köp för {{lamp.cost}} kronor</button>
            </div>
          </div>
          
        </div>
      </div>
      </div>
    </main>
    <div class="basket">
      
      <div class="overlay" data-click="hide"></div>
        <div id="cart" class="jumbotron corners padding transp">
          <h3>Varukorg</h3>
          <div v-for="(lamp, index) in purchasedLamps" :key="index">
            <div>
          <h5 class="d-flex justify-content-between">{{lamp.name}}<span>{{lamp.cost}}</span></h5>
            </div>
          </div>
          <ul>
            <li class="total">Total <span>{{totalPrice}}</span></li>
          </ul>
        </div>
     
    </div>
    </div>
</template>

<script>
export default{
data(){
  return{
    search: "",
    totalPrice: 0,
    purchasedLamps: [],
    lamps: [ 
      {
        name: 'Vit taklampa',
        id: '14',
        description: 'Mått Ø 25 cm, höjd 20 cm.',
        cost: 2500,
        image: 'https://d2lhb5rbruih0q.cloudfront.net/eyJ2IjoxMDIsInQiOiJwcm9kdWN0IiwibiI6IjEyMzEwMS5qcGcifQ==/34537.jpg?q=85&w=670&h=447&dpr=2',
        keywords: ['stor','20-tal']
       },
       {
         name: 'Bordslampa i guld',
        id: '9',
        description: 'Mått Ø 55 cm, höjd 30 cm.',
        cost: 6900,
        image: 'https://d2lhb5rbruih0q.cloudfront.net/eyJ2IjoxMDIsInQiOiJwcm9kdWN0IiwibiI6IjUyMzI0Ni5qcGcifQ==/107942.jpg?q=85&w=670&h=447&dpr=2',
        keywords: ['läslampa','80-tal']
       },
       {
        name: 'Vit golvlampa',
        id: '21',
        description: 'Mått Ø 15 cm, höjd 200 cm.',
        cost: 1780,
        image: 'https://d2lhb5rbruih0q.cloudfront.net/eyJ2IjoxMTMsInQiOiJwcm9kdWN0IiwibiI6IjEwNTQ2Ni5qcGcifQ==/5778.jpg?q=85&w=670&h=447&dpr=2',
        keywords: ['läslampa']
       }
       ]
}
},

methods: {
  buyLamp: function(lamp) {
    this.purchasedLamps.push(lamp)
    this.totalPrice += lamp.cost
  }

},
computed: {
  filteredLamps (){
    
          return this.lamps.filter(lamp => {
          return lamp.name.toLowerCase().includes(this.search.toLowerCase())
      })
      }
    }
}



</script>
