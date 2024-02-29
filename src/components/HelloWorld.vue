<template>
    <!-- <div :class="{'weather-container':true,''}"> Rain Clouds Clear Snow-->
    <div   :class="{'weather-container':true,'rain':weather.main && weather.weather[0].main=='Rain','clouds':weather.main && weather.weather[0].main=='Clouds','snow':weather.main && weather.weather[0].main=='Snow','clear':weather.main && weather.weather[0].main=='Clear'}"> 
    
     <div class="weather-wrap">
      <div class="search-box">
       <input type="text" placeholder="Search..." class="search-bar" 
        v-model="query" v-on:keypress="fetchWeather" />
      </div>
      <div class="weather-info" v-if="typeof weather.main!=='undefined'">
       <div class="location-box">
        <div class="location">{{weather.name}},{{weather.sys.country }}
        </div>
        <div class="date">{{ todaysDate() }}</div>
       </div>
       <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
        <div class="icon">
         <img :src="`${weather_icon}${weather.weather[0].icon}${'@2x.png'}`"/>
        </div>
       </div>
      </div>
    </div>
   </div>
   </template>


<script>
import axios from "axios";
export default {
data() {
return {
api_key: "27bcc252742830381afd6856832da01a",
url_base: "https://api.openweathermap.org/data/2.5/",
weather_icon: "http://openweathermap.org/img/wn/",
query: "",
weather: {},
};
},
methods: {
async fetchWeather(e) {
if (e.key == "Enter") {
let response = await axios.get(
`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
);
this.setResults(response.data);
}
},
setResults(returnedResponse) {
this.weather = returnedResponse;
},
todaysDate() {
const months = [
"Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov",
"Dec",];
const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
let d = new Date();
let month = months[d.getMonth()];
let day = days[d.getDay()];
let date = d.getDate();
let year = d.getFullYear();
return `${month} ${date} ${day} ${year}`;
},
},
};
</script>









<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300;500;700;900&display=swap");
* {
margin: 0;
padding: 0;
box-sizing: border-box;
font-family: "Montserrat";
}
.weather-container{
margin-left: 90%;
background-image: url("https://wjla.com/resources/media2/16x9/full/1015/center/80/69c14b32-c117-4f62-9ccc-ea7407dc70a3-large16x9_Untitleddesign.png");
background-size: cover;
background-position: center;
transition: 0.4s;
width: 375px;
/* margin: 0 auto; */
border-radius: 25px;
margin-top: 50px;
box-shadow: 0px 0px 30px #00000065;
}
.rain{
    background-image: url("https://wjla.com/resources/media2/16x9/full/1015/center/80/69c14b32-c117-4f62-9ccc-ea7407dc70a3-large16x9_Untitleddesign.png");
}
.snow{
    background-image: url("https://static01.nyt.com/images/2024/01/13/multimedia/13nat-weather-gjmw/13nat-weather-gjmw-mediumSquareAt3X.jpg");
}
.clouds{
    background-image: url("https://www.shutterstock.com/image-photo/storm-clouds-gather-over-road-600nw-2254809053.jpg");
}
.clear{
    background-image: url("https://st2.depositphotos.com/3562663/9369/i/450/depositphotos_93692884-clear-weather-sky-sun-on-blue-sky-with-clouds-sun-rays.jpg");
}
.weather-wrap {
height: 660px;
padding: 25px;
border-radius: 25px;
background-image: linear-gradient(
to bottom,
rgba(0, 0, 0, 0.15),
rgba(0, 0, 0, 0.4)
);
}
.search-box .search-bar {
display: block;
width: 100%;
padding: 15px;
color: #313131;
font-size: 20px;
appearance: none;
border: none;
outline: none;
background: none;
background-color: rgba(255, 255, 255, 0.5);
box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
border-radius: 10px;
transition: 0.4s;
}
.search-box .search-bar:focus {
box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
background-color: rgba(255, 255, 255, 0.75);
}
.location-box .location {
color: #fff;
font-size: 32px;
font-weight: 500;
font-style: italic;
text-align: center;
margin-top: 30px;
}
.location-box .date {
color: #fff;
font-size: 20px;
font-weight: 300;
text-align: center;
}
.weather-box {
text-align: center;
}
.weather-box .temp {
display: inline-block;
padding: 10px 25px;
color: #fff;
font-size: 102px;
font-weight: 900;
text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
background-color: rgba(255, 255, 255, 0.25);
border-radius: 16px;
margin: 30px 0px;
box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
font-style: italic;
}
.weather-box .weather {
color: #fff;
font-size: 48px;
font-weight: 700;
font-style: italic;
text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>