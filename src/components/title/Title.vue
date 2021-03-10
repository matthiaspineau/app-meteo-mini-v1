<template>
    <div class="wrapper__title">
        <h2 class="title__city">{{ file.name }}</h2>

        <div class="contain__center">
          <div class="left">
            <img
              :src="require('@/assets/icon_meteo/'+file.weather[0].icon+'.png')"
              alt=""
            />
          </div>

          <div class="right">
            <div class="desc">{{ file.weather[0].description }}</div>
            <div class="temp">{{ Math.round(file.main.temp_min) }}°</div>
          </div>
        </div>
    </div>
</template>

<script>
// let test = {
//     "clear sky": "ciel degager"
// }

export default {
    name: 'Title',
    props: {
        file: {
            type: Object,
            default: function () {
                return {}
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.wrapper__title {

    h2.title__city {
        margin: 0;
        padding-top: 15px;
        padding-bottom: 15px;
        font-size: 1.3rem;
        text-align: center;
    }

    .contain__center {
        padding-top: 15px;
        padding-bottom: 15px;
        display: flex;
        justify-content: center;

        .left, .right {
            min-width:50%;
            // border: 1px solid black;
        }

        .left {
            padding-left: 15px;
            padding-right: 10px;
        }

        .right {
            padding-top: 15px;
            padding-left: 25px;
        }


    }

    .desc {

    }

    .temp {
        font-size: 4.5rem;
    }
}
</style>