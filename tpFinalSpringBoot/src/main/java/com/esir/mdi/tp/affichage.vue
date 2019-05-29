<template>
<div>
 <div class="container" id="tuto">
      <br>
 
      <div class="panel panel-primary" v-show="personnes.length">
        <div class="panel-heading">Personnes actives</div>        
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
             <th class="col-sm-5">Nom</th>
             <th class="col-sm-5">Prénom</th>
             <th class="col-sm-2"></th>
             <th class="col-sm-2"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="personne in personnes">
              <td>{{ personne.nom }}</td>
              <td>{{ personne.prenom }}</td> 
              <td><button class="btn btn-warning btn-block" v-on:click="supprimer($index)">Poubelle</button></td>
              <td><button class="btn btn-warning btn-block" v-on:click="modifier($index)">Modifier</button></td>   
            </tr>  
          </tbody>       
        </table>
        <div class="panel-footer">
          &nbsp
          <button class="button btn btn-xs btn-warning" v-on:click="toutPoubelle">Tout à la poubelle</button>
        </div>
      </div> 
 
      

        <div class="panel panel-danger" v-show="p.length">
            <div class="panel-heading">personne</div>
            <table class="table table-bordered table-striped">
              <thead>
                <tr>
                 <th class="col-sm-4">Nom</th>
                 <th class="col-sm-4">Prénom</th>
                 <th class="col-sm-2"></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="per in p">
                  <td><input id="nom" v-model="prenom" type="text" name="nom" placeholder="{{ per.nom }}"> </td>
                  <td><input id="prenom" v-model="prenom" type="text" name="prenom" placeholder="{{ per.prenom }}"></td> 
                  <td><button class="btn btn-success btn-block" v-on:click="valider($index)">Valider</button></td>    
                </tr>  
              </tbody>       
            </table>
          </div>  


      <div class="panel panel-danger" v-show="poubelle.length">
        <div class="panel-heading">Poubelle</div>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
             <th class="col-sm-4">Nom</th>
             <th class="col-sm-4">Prénom</th>
             <th class="col-sm-2"></th>
             <th class="col-sm-2"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="personne in poubelle">
              <td>{{ personne.nom }}</td>
              <td>{{ personne.prenom }}</td> 
              <td><button class="btn btn-success btn-block" v-on:click="retablir($index)">Rétablir</button></td>
              <td><button class="btn btn-danger btn-block" v-on:click="eliminer($index)">Supprimer</button></td>    
            </tr>  
          </tbody>       
        </table>
        <div class="panel-footer">
          &nbsp
          <div class="btn-group">
            <button class="button btn btn-xs btn-success" v-on:click="toutRetablir">Tout rétablir</button>
            <button class="button btn btn-xs btn-danger" v-on:click="toutEliminer">Tout supprimer</button> 
          </div>
        </div>
      </div> 
 
    </div>
 </div>
</template>
<script src="http://cdn.jsdelivr.net/vue/1.0.10/vue.min.js"></script>
 
    <script>
 
      var vm = new Vue({
        el: '#tuto',
        data: {
        return {
          event: null,
          personnes: [],
          poubelle: [],
          p: []
          };
        },
          mounted() {
          axios.get("http://148.60.11.233/polls/" + this.$route.params.id).then(response => {
        this.event = response.data;
      });
    this.url = location.href;
    console.log(location.href);
  }
        methods: {
          supprimer: function(index) {
            this.poubelle.push(this.personnes[index]);
            this.personnes.splice(index, 1);
            this.poubelle.sort(ordonner);
          },
          retablir: function(index) {
            this.personnes.push(this.poubelle[index]);
            this.poubelle.splice(index, 1);
            this.personnes.sort(ordonner);
          },
          modifier: function(index) {
            this.p.push(this.personnes[index]);
            this.personnes.splice(index, 1);
            this.p.sort(ordonner);
          },
          retablir: function(index) {
            this.personnes.push(this.p[index]);
            this.p.splice(index, 1);
            this.personnes.sort(ordonner);
          },
          eliminer: function(index) {
            this.poubelle.splice(index, 1);
          },
          toutPoubelle: function() {
            this.poubelle = this.poubelle.concat(this.personnes);
            this.poubelle.sort(ordonner);
            this.personnes = [];
          },
          toutRetablir: function() {
            this.personnes = this.personnes.concat(this.poubelle);
            this.personnes.sort(ordonner);
            this.poubelle = [];
          },
          toutEliminer: function() {
            this.poubelle = [];
          }
        }
      });
 
      var ordonner = function (a, b) { return (a.nom > b.nom) };
 
    </script>
<style type="text/css">
    .header {
  background-color: #f44336;
  padding: 30px 40px;
  color: white;
  text-align: center;
}

/* Clear floats after the header */
.header:after {
  content: "";
  display: table;
  clear: both;
}

body{
    background-color: #5dade2;
    font-family: Helvetica, sans-serif;
}
    </style>
