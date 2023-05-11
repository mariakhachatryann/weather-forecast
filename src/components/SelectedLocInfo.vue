<template>
    <div class="forecast-table">
        <div class="container">
            <div class="forecast-container">
                <div class="today forecast">
                    <div class="forecast-header">
                        <div class="day">{{ weekDay }}</div>
                        <div class="date">{{ day }}</div>
                    </div>
                    <div class="forecast-content">
                        <div class="location">{{`${weatherDetails.location.name}/${weatherDetails.location.country}`}} </div>
                        <div>{{ weatherDetails.location.localtime }}</div>
                        <div class="degree">
                            <div class="num">{{ Math.round(parseInt(weatherDetails.current.temp_c)) }}<sup>o</sup>C</div>
                            <div class="forecast-icon">
                                <img :src="weatherDetails.current.condition.icon" alt="" width=90>
                            </div>
                        </div>
                        <div class="details">
                            <div class="details-text"><span>{{ weatherDetails.current.condition.text }}</span></div>
                            <span><img src="@/assets/images/icon-umberella.png" alt="">{{ weatherDetails.current.humidity }}%</span>
                            <span><img src="@/assets/images/icon-wind.png" alt="">{{ weatherDetails.current.wind_kph }}km/h</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["weatherDetails"],
    computed: {
        weekDay() {
            const weekday = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            return weekday[new Date().getDay()];
        },
        day() {
            const months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            return `${new Date().getUTCDate()} ${months[new Date().getMonth()]}`
        }
    }
}

</script>

<style scoped>
.forecast-container {
    width: 700px;
    background: #1e202b;
    display: table;
    table-layout: fixed;
    overflow: hidden;
    border-radius: 10px;
    margin-top: -150px;
    margin-bottom: 50px;
    margin: 5px auto;
    box-shadow: rgba(0, 0, 0, 0.10) 0px 10px 20px, rgba(0, 0, 0, 0.23) 0px 6px 6px;
}

.forecast-container .forecast.today .forecast-header:after {
    content: " ";
    clear: both;
    display: block;
    overflow: hidden;
    height: 0;
}

.forecast-container .forecast.today .forecast-header .day {
    float: left;
}

.forecast-container .forecast.today .forecast-header .date {
    float: right;
}

.forecast-container .forecast.today .forecast-content {
    text-align: left;
    padding-top: 30px;
    padding-bottom: 30px;
}

.forecast-container .forecast.today .location {
    font-size: 18px;
    font-size: 1.2857142857em;
    font-weight: 400;
}

.forecast-container .forecast.today .degree .num,
.forecast-container .forecast.today .degree .forecast-icon {
    display: inline-block;
    vertical-align: middle;
}

.forecast-container .forecast.today .degree .num {
    font-size: 87px;
    margin-right: 30px;
}

.forecast-container .forecast.today span {
    margin-right: 20px;
    font-size: 18px;
}

.forecast-container .forecast.today span img {
    margin-right: 5px;
    vertical-align: middle;
}

.forecast-container .forecast .forecast-header {
    background: rgba(0, 0, 0, 0.1);
    padding: 10px;
    text-align: center;
    font-weight: 400;
}

.forecast-container .forecast .forecast-icon {
    height: 50px;
}

.forecast-container .forecast .forecast-content {
    padding: 50px 20px 10px;
    text-align: center;
}

.forecast-container .forecast .forecast-content .degree {
    font-size: 24px;
    font-size: 1.7142857143em;
    color: white;
    font-weight: 700;
}

.forecast-container .forecast .forecast-content small {
    font-size: 20px;
    font-size: 1.1428571429em;
}

.forecast-container .forecast .forecast-content .location {
    font-size: 28px;
}

@media (max-width: 600px) {
    .forecast-container {
        display: block;
        width: 100%;
    }

    .details-text {
        margin: 15px;
    }
}
</style>