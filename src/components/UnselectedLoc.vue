<template>
    <div class="weather-info">
        <p class="weather-select">Please enter a location to see information</p>
        <div class="weather">
            <div class="anim weather-row"></div>
            <div class="anim weather-row"></div>
            <div class="anim weather-row"></div>
            <div class="anim weather-row"></div>
        </div>
    </div>
</template>

<style scoped>
.weather-info {
    box-shadow: 0 0 20px rgba(0, 0, 0, .25);
    padding: 25px;
    position:static;
    z-index: 5;
    width: 700px;
    background: #323544;
        border-radius: 10px;
    margin: 5px auto;
}

.weather-select {
    font-size: 18px;
    line-height: 24px;
    text-align: center;
}

.weather {
    margin-top: 30px;
}

.anim {
    animation: anim 1.5s ease-in-out .5s infinite;
}

.weather-wrap {
    grid-column-gap: 10px;
    align-items: center;
    -webkit-column-gap: 10px;
    column-gap: 10px;
    display: grid;
    grid-template-columns: 40px auto;
}

.weather-row {
    height: 35px;
    margin-top: 15px;
    background-color: #565b72;
    width: 100%;
}

@keyframes anim {
    0% {
        opacity: 1;
    }

    50% {
        opacity: .4;
    }

    100% {
        opacity: 1;
    }
}
@media (min-width: 768px) {
    .weather-info {
        width: 750px;
    }
}

@media (max-width: 600px) {
.weather-info {
    width: 350px;
}
}
</style>