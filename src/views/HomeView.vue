<template>
  <div>
    <!--<div>
      <h1>Burgers</h1>
        <Burger v-for="burger in burgers" 
              v-bind:burger="burger" 
              v-bind:key="burger.name"/> 
    </div>-->

   
  </div>
  <body>
    <section id="header1">
    <header>
        <img id="headerpic" src="https://tipbuzz.com/wp-content/uploads/Grilled-Burgers-thumbnail.jpg">
        <h1 id="he1">
            Välkommen till BURGERSTATION AB
        </h1>
        
       
    </header>
    </section>
    <main> 
        <section id="burgersection">
            <nav> MENU ITEMS </nav>
            <h3> SELECT BURGER </h3>
                <p> what burger do you want?</p>
    <div class="wrapper">
      <Burger v-for="burger in burgers" 
              v-bind:burger="burger" 
              v-bind:key="burger.name"
              v-on:orderedBurger="addToOrder($event)"/> 
<!--         <div class="box a">
            <h4> Dubbeltrubbel </h4>
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSiGh7FQlRgqiY7YMxMQFp58bHCOlj2w2wdBQ&usqp=CAU" alt="Span" title="test" style="width: 200px">
                <ul>
                    <li> Dubbelpuck </li>
                    <section class="Gluten">
                        <li> Gluten </li>
                    </section>
                    <li> Skön sås </li>
                    <li> Pommes </li>
                </ul>
        </div>
        <div class="box b">
            <h4> Burger-sandwich </h4>
            <img src="https://i0.wp.com/media.zeinaskitchen.se/2021/02/smashed-burgare-20.jpg?resize=1324%2C1500&ssl=1" alt="Span" title="test" style="width: 200px">
                <ul>
                    <section class="Laktos">
                        <li> Laktos </li>
                    </section>
                    <li> Ekonomiskt alternativ </li>
                    <li> haha </li>
                </ul>
        </div>
        <div class="box c">
            <h4> Halv-äten </h4>
            <img src="https://previews.123rf.com/images/dheeraj11/dheeraj111507/dheeraj11150700009/42134893-half-eaten-burger.jpg" alt="Span" title="test" style="width: 200px">
                <ul>
                    <li> Halv-äten burgare </li>
                    <li> För den som inte är så hungrig </li>
                    <li> Ingen ketchup </li>
                    <li> text3 </li>
                </ul>
        </div>
 -->
    </div>
        </section>
        
        <section id="customersection">
        <h3> CUSTOMER INFORMATION </h3>
        <p> Enter your information here</p>
        <p>
            <label for="First- and lastname">
                Full name:
            </label><br>
            <input type="text" id="First- and lastname" v-model="fln" required="required" placeholder="First- and last name">
            {{fln}}
        </p>
        <p>
            <label for="Email">
                E-mail:
            </label><br>
            <input type="email" id="Email" v-model="em" required="required" placeholder="E-mail address">
            {{em}}
        </p>
       <!--<p>
            <label for="Street">
                Street:
            </label><br>
            <input type="text" id="Street" v-model="st" required="required" placeholder="Address">
            {{st}}
        </p>
        <p>
            <label for="HOUSENUM">
                House number:
            </label><br>
            <input type="number" id="HOUSENUM" v-model="hn" required="required" placeholder="123">
            {{hn}}
        </p> --> 
        <p>
            <label for="recipient">Payment method</label><br>
            <select id="recipient" v-model="rcp">
                <option>Visa</option>
                <option>Mastercard</option>
                <option>Swish</option>
                <option>Klarna</option>
            </select>
            {{rcp}}
         </p>
         <p> Select gender </p>
         <p>
            <label for="gender">
                Male
            </label>
            <input type="radio" id="gender" v-model="gr" value="male">
            {{gr}}
        </p>
        <p>
            <label for="gender">
                Female
            </label>
            <input type="radio" id="gender" v-model="gr" value="female">
            {{gr}}
        </p>
        <p>
            <label for="gender">
                Other
            </label>
            <input type="radio" id="gender" v-model="gr" value="other">
            {{gr}}
        </p>
        <p>
            <label for="gender">
                Undisclosed
            </label>
            <input type="radio" id="gender" v-model="gr" checked="checked" value="undisclosed">
            {{gr}}
        </p>
        <div class="mapWrap">
          Välj leverans:
        <div id="map" v-on:click="setLocation">
          <div v-bind:style="{ left: this.location.x + 'px', top: this.location.y + 'px'}">
            <span>T</span>
            </div>
    </div>
  </div>
        </section>
        <button type="submit" id="buybutton" v-on:click="order">
            <img src="https://img.fruugo.com/product/6/86/618064866_max.jpg" style="width: 30px">
            PURCHASE 
          </button>
        
    </main>
     
    <footer>
        Burgerstore AB Copyrighted Content
    </footer>
    
   </body>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import menu from '../assets/menu.json'
import io from 'socket.io-client'


const socket = io();

/* function MenuItem(name, imageURL, kCal, containsGluten, containsLactose) {
  this.name = name;
  this.imageURL = imageURL;
  this.kCal = kCal;
  this.containsGluten = containsGluten;
  this.containsLactose = containsLactose;
 }*/
/* const arrayOfBurgers = [
  new MenuItem("Barger", "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSiGh7FQlRgqiY7YMxMQFp58bHCOlj2w2wdBQ&usqp=CAU", 300, true, false),
  new MenuItem("Birger", "https://i0.wp.com/media.zeinaskitchen.se/2021/02/smashed-burgare-20.jpg?resize=1324%2C1500&ssl=1", 400, true, true),
  new MenuItem("Berger", "https://previews.123rf.com/images/dheeraj11/dheeraj111507/dheeraj11150700009/42134893-half-eaten-burger.jpg", 500, false, false)
];

console.log(arrayOfBurgers); */

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers:menu,
      fln: '',
      em: '',
      //st: '',
      //hn: '',
      rcp: '',
      gr: '',
      orderedBurgers: {},
      location: { x: 0, y: 0 }
      
      
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    
    //addOrder: function (event) {
      //var offset = {x: event.currentTarget.getBoundingClientRect().left,
        //            y: event.currentTarget.getBoundingClientRect().top};
      //this.location = { x: event.clientX - 20 - offset.x, y: event.clientY - 10 - offset.y },
      //socket.emit("addOrder", { orderId: this.getOrderNumber(),
        //                        details: { x: event.clientX - 10 - offset.x,
          //                                 y: event.clientY - 10 - offset.y },
            //                    orderItems: ["Beans", "Curry"]
              //                }
                // );
    //},
    setLocation: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      this.location = { x: event.clientX - 20 - offset.x, y: event.clientY - 10 - offset.y }
      console.log(this.location)
    },
    order: function (event) {
      console.log(this.fln, this.em, this.st, this.hn, this.rcp, this.gr),
      console.log(this.orderedBurgers),
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: this.location.x,
                                           y: this.location.y },
                                orderItems: this.orderedBurgers,
                                personalInformation: {fln: this.fln, 
                                                      em:  this.em, 
                                                      rcp: this.rcp,
                                                      gr:  this.gr}
                              }
                 );
    },
    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
      console.log(this.orderedBurgers)
      
},
  }
}
</script>

<style>
  
  /* Your comment goes here */
body {
    font-family: "Bodoni MT";
    color: blueviolet;
    .Gluten {
        font-weight: bold;
        color: blueviolet;
    }
    .Laktos {
        font-weight: bold;
        color: mediumvioletred;
    }
    #burgersection {
        color: white;
        background-color: black;
        margin: 10px;
        padding-left: 20px;
        padding-right: 20px; 
        padding-top: 10px; 
        padding-bottom: 1px;
        border: 7px dashed blueviolet;
    }
    #customersection {
        margin: 10px;
        padding-left: 20px;
        padding-right: 20px;
        padding-top: 1px;
        padding-bottom: 10px;
        border: 7px dashed blueviolet;
    }
    #map {
    
    width: 1920px;
    height: 1078px;
    background: url("../../public/img/polacks.jpg");
    
   
  }
  #map div {
    position: relative;
  }
  .mapWrap {
    width: 500px;
    height: 500px;
    overflow: scroll
  }
   
}
button:hover {
    background-color: blueviolet;
    cursor: wait;
}
#buybutton {
    margin: 10px;
}

div * {
    margin-left: 10px;
    margin-top: 1px;
}
#header1 {
    margin: 10px;
    height: 100px;
    overflow:hidden
}


#headerpic {
    opacity: 0.5;
    width: 100%;
    height: auto;
}

#he1 {
    position: absolute;
    margin: 10px;
    margin-top: -475px;
}
.wrapper {
    display: grid;
    grid-gap: 10px;
    grid-template-columns: 200px 200px 200px;
    
}


</style>