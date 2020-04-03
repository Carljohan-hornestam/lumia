<template>
  <div class="page corners padding transp">
  <header><nav class="nav flex-column flex-sm-row">
  <router-link class="flex-sm-fill flex-grow-1 text-sm-left nav-link active" to="/"><h1>{{homeLink}}</h1></router-link>
  <router-link class="text-sm-right nav-link" to="/Contact">{{contactLink}}</router-link>
</nav></header>
<main><div class="contact">
  <div class="form-group">
    <label for="exampleFormControlInput1">Din email</label>
    <input type="email" class="form-control" id="exampleFormControlInput1" placeholder="namn@exempel.se">
  </div>
  <div class="form-group">
    <label for="exampleFormControlTextarea1">Ditt meddelande</label>
    <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
  </div>
  <div class="d-flex justify-content-end">
    <button type="button" class="btn btn-outline-dark">Skicka ditt meddelande</button>
  </div>
</div>
</main>
    <div class="basket">
      <div class="overlay" data-click="hide"></div>
        <div id="cart" class="jumbotron corners padding transp">
          <h3>Varukorg</h3>
          <ul>
            <li class="total">Total <span>0</span></li>
          </ul>
        </div>
      </div>
    </div>
</template>
<script>
export default {

  data(){
    return {
      homeLink: 'Lumia',
      contactLink: 'Kontakta oss'
    }
  }

}

</script>
