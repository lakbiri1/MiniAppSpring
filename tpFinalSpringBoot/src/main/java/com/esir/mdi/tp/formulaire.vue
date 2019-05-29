<template>
<div class="event">
  <section class="login-container">
         <div id="myDIV" class="header">
  <h2>Createur</h2>
  <div id="main">
            <form action="" method="post">
                <input id="nom" v-model="prenom" type="text" name="nom" placeholder="Saisir votre nom" required>
                <input id="prenom" v-model="prenom" type="text" name="prenom" placeholder="Saisir votre prenom" required>
                <input id="lieu" v-model="lieu" type="text" name="lieu" placeholder="Lieu (facultatif)">
                <input id="tel" v-model="tel" type="text" name="tel" placeholder="Saisir votre telephone" required>
                <input id="mail" v-model="mail" type="email" name="mail" placeholder="saisir votre mail" required>
                <input type="date" v-model="jour" required><input type="time" v-model="heure" required>
                <button type="submit">Continue</button>

            </form>
          </div>
</div>

    </section>
</div>
</template>
<script>
import axios from "axios";
export default {
  name: "event",
  data() {
    return {
      nom: null,
      prenom: null,
      lieu: null,
      tel: null,
      mail: null,
      jour: null,
      heure: null,
      id: null
    };
  },
  methods: {
    submitForm(e) {
      e.preventDefault();
      axios
        .post("http://148.60.11.233/polls", {
          nom: this.nom,
          prenom: this.prenom,
          lieu: this.lieu,
          tel: this.tel,
          mail: this.mail,
          jour: this.jour,
          heure: this.heure
        })
        .then(response => {
          this.$router.push({ name: "aff", params: { id: response.data.id } });
        });
    }
  }
};
</script>
<style type="text/css">
section.login-container{
    display: flex;
    position: fixed;
    top:0;
    left: 0;
    bottom: 0;
    right: 0;
  
    background:  #f0b27a ;
}
section.login-container > div{
    width: 450px;
  
    margin: auto;
  
    padding: 20px;

    text-align: center;

    background:  #f44336;
    border: 1px solid #ccc;

    border-radius: 5px;

}
section.login-container form{
    display: flex;
    flex-direction: column;
}
form input[type="email"], 
form input[type="text"], 
form button[type="submit"] {
    width: 100%;
  
    margin-bottom: 32px;
    padding: 16px;
  
    color: #333;

    border: 1px solid #ccc;
    border-radius: 5px;

    outline: 0;
}


form input[type="text"]:focus,
form input[type="text"]:hover,
form input[type="password"]:focus,
form input[type="password"]:hover {
    background-color: white;
}

form button[type="submit"] {
    font-weight: bold;
    color: #f44336;
    text-transform: uppercase;

    background-color: #f44336;
}
form button[type="submit"]:focus,
form button[type="submit"]:hover {
    background-color: #d35400;
}

/* Include the padding and border in an element's total width and height */
* {
  box-sizing: border-box;
}

/* Remove margins and padding from the list */
ul {
  margin: 0;
  padding: 0;
}

/* Style the list items */
ul li {
  cursor: pointer;
  position: relative;
  padding: 12px 8px 12px 40px;
  background: #eee;
  font-size: 18px;
  transition: 0.2s;

  /* make the list items unselectable */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Set all odd list items to a different color (zebra-stripes) */
ul li:nth-child(odd) {
  background: #f9f9f9;
}

/* Darker background-color on hover */
ul li:hover {
  background: #ddd;
}

/* When clicked on, add a background color and strike out text */
ul li.checked {
  background: #888;
  color: #fff;
  text-decoration: line-through;
}

/* Add a "checked" mark when clicked on */
ul li.checked::before {
  content: '';
  position: absolute;
  border-color: #fff;
  border-style: solid;
  border-width: 0 2px 2px 0;
  top: 10px;
  left: 16px;
  transform: rotate(45deg);
  height: 15px;
  width: 7px;
}

/* Style the close button */
.close {
  position: absolute;
  right: 0;
  top: 0;
  padding: 12px 16px 12px 16px;
}

.close:hover {
  background-color: #f44336;
  color: white;
}

/* Style the header */
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
/* Style the input */
input {
  margin: 0;
  border: none;
  border-radius: 0;
  width: 75%;
  padding: 10px;
  float: left;
  font-size: 16px;
}

/* Style the "Add" button */
.addBtn {
  padding: 10px;
  width: 25%;
  background: #d9d9d9;
  color: #555;
  float: left;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 0;
}
form button[type="submit"] {
    width: 100%;
  
    margin-bottom: 32px;
    padding: 16px;
  
    color: #333;

    border: 1px solid #ccc;
    border-radius: 5px;

    outline: 0;
}

form button[type="submit"] {
    font-weight: bold;
    color: #eee;
    text-transform: uppercase;

    background-color: white;
}

form button[type="submit"]:focus,
form button[type="submit"]:hover {
    background-color: #d35400;
}

.addBtn:hover {
  background-color: #bbb;
}
</style>
