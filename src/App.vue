<template>
    <base-dialog :show="showDialog" title="Not Found" @close="tryClose">
        No information found of entered location...
    </base-dialog>
    <div class="app-name">
        <h1>Weather Forecast</h1>
    </div>
    <div class="search">
        <div class="container">
            <form action="#" class="find-location" @submit.prevent="findLocation">
                <input type="text" placeholder="Find your location..." v-model="location">
                <input type="submit" value="Find">
            </form>
        </div>
    </div>
    <base-spinner v-if="spinnerVisibility"></base-spinner>
    <unselected-loc v-if="notVisible && !spinnerVisibility"></unselected-loc>
    <selectedloc-info v-else-if="!spinnerVisibility" :weatherDetails="weatherDetails"></selectedloc-info>
</template>

<script>
import UnselectedLoc from "@/components/UnselectedLoc.vue";
import SelectedlocInfo from "@/components/SelectedLocInfo.vue";
import BaseSpinner from "@/components/BaseSpinner.vue";
import BaseDialog from "@/components/BaseDialog.vue";

export default {
    components: {
        UnselectedLoc, SelectedlocInfo, BaseSpinner, BaseDialog
    },
    data() {
        return {
            location: "",
            weatherDetails: {},
            notVisible: true,
            spinnerVisibility: false,
            showDialog: false
        }
    },
    methods: {
        async findLocation() {
            this.spinnerVisibility = true;
            const API_KEY = "05add20bc4874a9dadb104317233004";
            try {
                const response = await fetch(`https://api.weatherapi.com/v1/current.json?key=${API_KEY}&q=${this.location}`);
                if (response.ok) {
                    this.weatherDetails = await response.json();
                    this.location = "";
                    this.notVisible = false;

                    console.log(this.weatherDetails)
                } else {
                    throw new Error(`Request failed with status ${response.status}`);
                }
            } catch (error) {
                this.showDialog = true;
                this.notVisible = true;
            } finally {
                this.spinnerVisibility = false;
            }
        },
        tryClose() {
            this.showDialog = false
            this.location = "";
        }
    }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap");

body {
    color: #bfc1c8;
    font-family: "Roboto", "Open Sans", sans-serif;
    font-size: 14px;
    font-weight: 300;
    line-height: 1.5;
    background: #5d5858;
}

form,
input {
    border-radius: 30px;
    outline: none;
}

.app-name {
    color: #fff;
    padding: 10px;
    border-radius: 6px;
}

.app-name h1 {
    font-size: 37px;
    text-align: center;
}

.search {
    background-size: cover;
    padding: 10px 0 50px 0;
}

.container {
    margin-right: auto;
    margin-left: auto;
    padding-left: 15px;
    padding-right: 15px;
    *zoom: 1;
}

.container:after {
    content: " ";
    clear: both;
    display: block;
    overflow: hidden;
    height: 0;
}

.find-location {
    position: relative;
    display: flex;
    justify-content: center;
}

.find-location input[type="text"] {
    flex: 1;
    padding: 20px;
    background: #1e202b;
    color: white;
    font-size: 20px;
    outline: none;
    border: none;
    border-radius: 5px 0 0 5px;
}

.find-location input[type="submit"] {
    border: none;
    background: #323544;
    color: white;
    font-size: 20px;
    padding: 0 40px;
    cursor: pointer;
    border-radius: 0 5px 5px 0;
}

@media (max-width: 600px) {
    .find-location {
        flex-direction: column;
        align-items: center;
    }

    .find-location input[type="text"] {
        width: 100%;
        border-radius: 5px;
        margin-bottom: 5px;
    }

    .find-location input[type="submit"] {
        width: 100%;
        border-radius: 5px;
    }
}

@media (min-width: 768px) {
    .container {
        width: 750px;
    }
}

@media (min-width: 992px) {
    .container {
        width: 970px;
    }
}

@media (min-width: 1200px) {
    .container {
        width: 1170px;
    }
}
</style>
