<template>
  <div class="page corners padding transp">
  <header><nav class="nav flex-column flex-sm-row">
  <router-link class="flex-sm-fill flex-grow-1 text-sm-left nav-link active" to="/"><h1>{{homeLink}}</h1></router-link>
  <router-link class="text-sm-right nav-link" to="/Contact">{{contactLink}}</router-link>
</nav></header>
<main><div class="contact">
  <form id="inputForm">
  <div class="form-group">
    <label for="exampleFormControlInput1">Din email</label>
    <input type="email" class="form-control" id="exampleFormControlInput1" placeholder="namn@exempel.se">
  </div>
  <div class="form-group">
    <label for="exampleFormControlTextarea1">Ditt meddelande</label>
    <textarea class="form-control" id="exampleFormControlTextarea1"  rows="3"></textarea>
  </div>
  <div class="d-flex justify-content-end">
    <button type="button" v-on:click="contactConfirmation()" class="btn btn-outline-dark">Skicka ditt meddelande</button>
  </div>
  </form>
</div>
</main>
    
    </div>
</template>
<script>
export default {

  data(){
    return {
      homeLink: 'Lumia',
      contactLink: 'Kontakta oss'
    }
  },
  methods: {
    contactConfirmation(){
      document.getElementById('exampleFormControlInput1').value = ""
      document.getElementById('exampleFormControlTextarea1').value = ""

      alert('Tack för ditt meddelande! Vi kommer att kontakta dig snarast :))')
    }
  }

}

</script>
