<template>
  <div class="Home">
    <div >
      <caption>Розклад перегонів на змаганнях "Piston Cup"</caption> 
      <table class="table table-striped">
        <thead>
          <tr>
              <th rowspan="2" class="first">Дата</th>
              <th colspan="2">Гонщик №1</th>
              <th colspan="2">Гонщик №2</th>
              <th rowspan="2">Траса</th>
            </tr>
            <tr>
              <td class="first">Автомобіль №1</td>
              <td class="first">Ім'я гонщика №1</td>
              <td class="first">Автомобіль №2</td>
              <td class="first">Ім'я гонщика №2</td>
            </tr>      
        </thead>
        <tbody>
          <Loader v-if="loading"/>
          <tr v-for="getMenu in menu" :key="getMenu.nameKitchen">
              <th scope="row" class="first">{{getMenu.nameKitchen}}</th>
              <th>{{getMenu.saladName}}</th>
              <th>{{getMenu.Snack}}</th>
              <th>{{getMenu.firstCourse}}</th>
              <th>{{getMenu.secondCourse}}</th>
              <th>{{getMenu.Dessert}}</th>
              <h6 v-on:click="Delete(getMenu._id)"> &#10006;</h6>
          </tr>
        </tbody>
      </table>
    </div>
     
  </div>
</template>

<script>
import Loader from './Loader/Loader'
export default {
  name: "Home",
  data(){
        return {
            menu:[],
            loading:true,
        }
  },
  mounted(){
      fetch('http://localhost:4000/app/getMenu')
      .then(response => response.json())
      .then(json=>{
          this.menu=json.menu
          console.log(json)
          this.loading = false
      })
      
  },
  components: {
   Loader,
  },
  methods:{
    addMenu(newMenu){
      this.menu.push(newMenu)
    },
    removeBlog(_id){
      this.blogs = this.blogs.filter(t=>t._id !==_id)
    },
    Delete(_id){
      fetch("http://localhost:4000/app/deleteMenu/"+_id, {
                method: 'DELETE'
            }).then(() => {
                console.log('removed');
            }).catch(err => {
                console.error(err)
            });
      this.menu = this.menu.filter(t=>t._id !==_id)
    }
  }
};
</script>

<style>
body {
  margin: 0;
  background: radial-gradient(#fff299, #fd2d2d); }
h6:hover{
  cursor: pointer;
  color: aqua;
}
table {
  border-collapse: collapse;
  line-height: 1.1;
  font-family: "Lucida Sans Unicode", "Lucida Grande", sans-serif;
  background: radial-gradient(farthest-corner at 50% 50%, white, #DCECF8);
  color: #0C213B; }

caption {
  font-family: times new roman, cursive;
  font-weight: bold;
  font-size: 2em;
  display: flex;
  padding: 10px;
  color: #fdd000;
  text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.3); }
  caption:before, caption:after {
    color: #A9E2CC;
    margin: 0 10px; }

th {
  padding: 10px;
  border: 1px solid #d5ebe3; 
  display:table-cell;
  }
  

td {
  font-size: 0.8em;
  padding: 5px 7px;
  border: 1px solid #A9E2CC; }

.first {
  font-size: 1em;
  font-weight: bold;
  text-align: center; }

</style>
