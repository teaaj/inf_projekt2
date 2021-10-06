<template>
  <div id="app" class="container">
    <nav class="navbar navbar-inverse">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="#">FOOD-RECIPE-NUTRITION</a>
        </div>
        <form class="navbar-form navbar-left" action="/action_page.php">
          <div class="input-group">
            <input
              type="text"
              class="form-control"
              placeholder="Search"
              name="search"
              style="height:56px"
              v-model="pretraga"
            />
            <div class="input-group-btn">
              <div class="dropdown">
                <button class="dropbtn">Search by</button>
                <div class="dropdown-content">
                  <a href="#" v-on:click="prvoSlovo">First latter</a>
                  <a href="#" v-on:click="ime">Name</a>
                </div>
              </div>
            </div>
          </div>
        </form>
      </div>
    </nav>
    <br />
    <br />
    <br />
    <br />
    <h1 style="text-align:center">
      <b>Welcome to The Food-Recipe-Nutrition</b>
    </h1>
    <br />
    <br />
    <h3 style="text-align:center">
      <b>
        <em>Welcome to the best recipe page. Here you can find most popular recipe in whole wide world!</em>
      </b>
    </h3>
    <br />
    <br />
    <br />
    <b-button
      variant="dark"
      style="width:250px; height:50px; background-color:blue; margin-left:390px"
      v-on:click="randomRecipe"
    >Click me for random Recipe!</b-button>

    <br />
    <br />
    <br />

    <b-row>
      <b-col cols="3" v-for="meal in recepti" v-bind:key="meal.idMeal">
        <div>
          <b-card
            :title="meal.strMeal"
            :img-src="meal.strMealThumb"
            img-top
            style="max-width: 20rem;"
            class="mb-2"
          >
            <b-card-text>{{ meal.strInstructions }}</b-card-text>
          </b-card>
        </div>
      </b-col>
      <b-col v-if="recepti == null" cols="2">
          <p style="color: white; background-color: black">No results.</p>
        </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function() {
    return {
      pretraga: "",
      recepti: []
    };
  },
  methods: {
    prvoSlovo: function() {
      this.axios
        .get(
          "https://www.themealdb.com/api/json/v1/1/search.php?f=" +
            this.pretraga
        )
        .then(response => {
          console.log(response.data.meals);

          this.recepti = response.data.meals;
        });
    },
    ime: function() {
      this.axios
        .get(
          "https://www.themealdb.com/api/json/v1/1/search.php?s=" +
            this.pretraga
        )
        .then(response => {
          console.log(response.data.meals);

          this.recepti = response.data.meals;
        });
    },
    randomRecipe: function() {
      this.axios
        .get("https://www.themealdb.com/api/json/v1/1/random.php")
        .then(response => {
          console.log(response.data.meals);

          this.recepti = response.data.meals;
        });
    }
  }
};
</script>
<style>
.dropbtn {
  background-color: blue;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}
.dropdown {
  position: relative;
  display: inline-block;
}
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}
.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}
.dropdown-content a:hover {
  background-color: #f1f1f1;
}
.dropdown:hover .dropdown-content {
  display: block;
}
.dropdown:hover .dropbtn {
  background-color: blue;
}
body {
  background-image: url("https://resize.hswstatic.com/w_907/gif/now-bf4a9734-a6e6-4aeb-b7df-8d320a4e40f2-1210-680.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
h1 {
  color: white;
  font-family: initial;
  background-color: black;
}
h3 {
  color: white;
  font-family: initial;
  background-color: black;
}
</style>
