<template>
  <div class="page corners padding transp">
    <header>
      <nav class="nav flex-column flex-sm-row">
        <router-link class="flex-sm-fill flex-grow-1 text-sm-left nav-link active" to ="/"><h1>Lumia</h1></router-link>
        <router-link class="text-sm-right nav-link" to="/Contact">Kontakta oss</router-link>
        <button class=" cartText" v-on:click="isHidden = false">Varukorg</button>

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
    <div class="basket" v-show="!isHidden">
      
      <div class="overlay" data-click="hide" v-on:click="isHidden = true"></div>
        <div id="cart" class="jumbotron corners padding transp">
          <h3>Varukorg</h3>
          <div v-for="(lamp, index) in purchasedLamps" :key="index">
            <div>
          <h5 class="d-flex justify-content-between">{{lamp.name}}
            <span class="d-flex justify-content-between" v-if="lamp.quantity < 2"><button class="removeOneItem" 
            @click="removeOneLamp(lamp)">-</button>{{lamp.cost}}</span>
          <span class="d-flex justify-content-between" v-if="lamp.quantity > 1"><button class="removeOneItem" 
          @click="removeOneLamp(lamp)">-</button>{{lamp.quantity}} x {{lamp.cost}}</span></h5>
            </div>
          </div>
          <ul>
            <li class="total">Total <span>{{totalPrice}}</span></li>
          </ul>
          <div class="d-flex justify-content-between">
          <span><button @click="emptyCart()">Töm varukorg</button></span>
          <span><button @click="order()">Beställ</button></span>
          </div>
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
    isHidden: true,
    purchasedLamps: [],
    lamps: [ 
      {
        name: 'Vit taklampa',
        id: '14',
        description: 'Mått Ø 25 cm, höjd 20 cm.',
        cost: 2500,
        quantity: 0,
        image: 'https://d2lhb5rbruih0q.cloudfront.net/eyJ2IjoxMDIsInQiOiJwcm9kdWN0IiwibiI6IjEyMzEwMS5qcGcifQ==/34537.jpg?q=85&w=670&h=447&dpr=2',
        keywords: ['stor','20-tal']
       },
       {
         name: 'Bordslampa i guld',
        id: '9',
        description: 'Mått Ø 55 cm, höjd 30 cm.',
        cost: 6900,
        quantity: 0,
        image: 'https://d2lhb5rbruih0q.cloudfront.net/eyJ2IjoxMDIsInQiOiJwcm9kdWN0IiwibiI6IjUyMzI0Ni5qcGcifQ==/107942.jpg?q=85&w=670&h=447&dpr=2',
        keywords: ['läslampa','80-tal']
       },
       {
        name: 'Vit golvlampa',
        id: '21',
        description: 'Mått Ø 15 cm, höjd 200 cm.',
        cost: 1780,
        quantity: 0,
        image: 'https://d2lhb5rbruih0q.cloudfront.net/eyJ2IjoxMTMsInQiOiJwcm9kdWN0IiwibiI6IjEwNTQ2Ni5qcGcifQ==/5778.jpg?q=85&w=670&h=447&dpr=2',
        keywords: ['läslampa']
       }
       ]
}
},

methods: {
  buyLamp: function(lamp) {
    this.totalPrice += lamp.cost
    this.isHidden = false;
    
    if (this.purchasedLamps.length < 1){
      this.purchasedLamps.push(lamp)
      lamp.quantity++
    }
    
    else{

      if (this.purchasedLamps.includes(lamp)){
          lamp.quantity++ 

      }
      else{
          this.purchasedLamps.push(lamp)
          lamp.quantity++
      }
  }
  },
  removeOneLamp(lamp){
    if (lamp.quantity == 1){
      console.log('i första if')
      let idtoRemove = lamp.id;
      this.purchasedLamps = this.purchasedLamps.filter((product) => product.id!== idtoRemove)
      this.totalPrice -= lamp.cost
    }
    else{
    lamp.quantity--
    this.totalPrice -= lamp.cost
  }
  
  },

  emptyCart(){
    this.purchasedLamps = []
    this.totalPrice = 0
  },

  order(){
    alert('Tack för din beställning!')
    this.purchasedLamps = []
    this.totalPrice = 0
  }

},
computed: {
  filteredLamps (){
    return this.lamps.filter(lamp => {
    let keywordsString = lamp.keywords.toString()
    return lamp.name.toLowerCase().includes(this.search.toLowerCase()) || keywordsString.toLowerCase()
    .includes(this.search.toLowerCase())
      })
      }
    }
}



</script>
