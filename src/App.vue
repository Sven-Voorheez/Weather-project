
<template>
  <div class="wrapper">
      <h1>Погодное приложение </h1>
      <p>Узнать погоду в {{ city == "" ? "в вашем городе" :  city }}</p>
      <input type="text" v-model="city" placeholder="Ведите город">
      <button v-if="city != '' " @click="getWeather()">Получить погоду</button>
      <button  disabled v-else>Введите название города</button>
      <p class="error">{{ error }}</p>
  
      <div   v-if="info != null">
          <p class="wet" >{{ ShowTemp }}</p>
          <p class="wet">{{ ShowFeelsLike }}</p>
          <p class="wet">{{ ShowMinTemp }}</p>
          <p class="wet">{{ ShowMaxTemp }}</p>
      </div>
      
  
  </div>
  
  </template>
  
  <script >
  import axios from 'axios'
  
  export default{
      data(){
          return{
              city: "",
              error: "",
              info: null
          }
      },
          computed:{
              cityName(){
                  return "| " + this.city + " |"
              },
              ShowTemp(){
                  return " Температура: " + this.info.main.temp 
              },
              ShowFeelsLike(){
                  return  " Ощющаеться : " + this.info.main.feels_like 
              },
              ShowMinTemp(){
                  return "Минимальная температура: " + this.info.main.temp_min
              },
              ShowMaxTemp(){
                  return "Максимальная температура: " + this.info.main.temp_max
              },
  
          },
          methods:{
              getWeather(){
  if(this.city.trim().length < 2){
      this.error = "Нужно название более 1 символа";
      return false;
  }
  this.error="";
  
  axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=df308833af70b7c0fe5a286261e84837`)
              .then(res =>(this.info = res.data))
  }
          }
  }
  
  </script>
  
  
  
  <style scoped>
  
  .wrapper{
      width: 900px;
      height: 500px;
      border-radius: 50px;
      background: rgb(2,0,36);
      background: linear-gradient(315deg, rgba(2,0,36,1) 0%, rgba(37,171,181,0.832545518207283) 35%, rgba(0,212,255,1) 100%);
  padding: 20px;
  text-align: center;
  color: aliceblue;
  }
  
  .wrapper h1{
      margin-top: 50px;
  }
  .wrapper h1{
      margin-top: 25px;
  }
  .wrapper input{
      margin-top: 30px;
      border: 0;
      border-radius: 20px;
      color: rgb(0, 0, 0);
      font-size: 15px;
      outline:none;
      padding: 5px;
  }
  
  .wrapper input:focus{
      border-bottom-color:black
  }
  
  .wrapper button{
      background: blueviolet;
      color: blanchedalmond;
      border-radius: 10px;
      border:2px solid black;
      padding: 10px;
      margin-left: 20px;
      cursor: pointer;
      transition: transform 500ms ease;
  }
  
  .wrapper button:hover{
      transform: scale(1.1) translateY(-5px);
  }
  .error{
      color: black;
  }
  .wet{
      color: black;
      font-size: 20px;
      margin-top: 15px;
  }
  </style>