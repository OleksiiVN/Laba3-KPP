<template>
  <div class="culture">
    <div>
      <form>
        <table>
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
        <tr>
          <td rowspan="3" class="first"><input type="text" v-model="nameKitchen" placeholder="Дата"></td>
          <td><input type="text" v-model="saladName" placeholder="Назва"></td>
          <td><input type="text" v-model="Snack" placeholder="Ім'я"></td>
          <td><input type="text" v-model="firstCourse" placeholder="Назва"></td>
          <td><input type="text" v-model="secondCourse" placeholder="Ім'я"></td>
          <td><input type="text" v-model="Dessert" placeholder="Назва"></td>
        </tr>
        </table>
        <button v-on:click="onSubmit" type="submit">Додати</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Culture",
   data(){
        return{
            nameKitchen:'',
            saladName:'',
            Snack:'',
            firstCourse:'',
            secondCourse:'',
            Dessert:''
        }
    },
   methods:{
        onSubmit(){
            if(this.nameKitchen.trim()){
                console.log(this.title)
                const newMenu = {
                    nameKitchen:this.nameKitchen,
                    saladName:this.saladName,
                    Snack:this.Snack,
                    firstCourse:this.firstCourse,
                    secondCourse:this.secondCourse,
                    Dessert:this.Dessert
                }
                console.log(newMenu)
                 fetch("http://localhost:4000/app/menu",{
                    method:'POST',
                    headers:{
                        'Content-Type': 'application/json',
                        'Accept': 'application/json'
                    },
                    body:JSON.stringify(newMenu)
                    })
                    .then(res=>{
                            res.json()
                        }
                    )
                  this.nameKitchen='';
                  this.saladName='';
                  this.Snack='';
                  this.firstCourse='';
                  this.secondCourse='';
                  this.Dessert=''
            }
        }
    }
};
</script>

<style>
table {
  border-collapse: collapse;
  line-height: 1.1;
  font-family: "Lucida Sans Unicode", "Lucida Grande", sans-serif;
  background: #cf0303;
  color: #0C213B; }
th {
  padding: 10px;
  border: 1px solid #A9E2CC; }

td {
  font-size: 0.8em;
  padding: 5px 7px;
  border: 1px solid #A9E2CC; }
input{
  width: 60px;
}
</style>
