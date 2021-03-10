<template>
    <div class="wrapper__table">
        <div class="table__top">
          <div class="table__card">
            <SvgMinTemp></SvgMinTemp>
            <span class="valeur">{{ file.main.temp_min }} °</span>
            <span class="small">{{ lang.min }}</span>
          </div>
          <div class="table__card">
            <SvgMaxTemp></SvgMaxTemp>
            <span class="valeur">{{ file.main.temp_max }} °</span>
            <span class="small">{{ lang.max }}</span>
          </div>
          <div class="table__card">
            <SvgBarometer></SvgBarometer>
            <span class="valeur">{{ file.main.pressure }}</span>
            <span class="small">{{ lang.pressure }}</span>
          </div>


          <div class="table__card">
            <SvgDrop></SvgDrop>
            <span class="valeur">{{ file.main.humidity }} %</span>
            <span class="small">{{ lang.humidity }}</span>
          </div>

          <div class="table__card">
            <SvgWind></SvgWind>
            <span class="valeur">{{ file.wind.speed }} km/h</span>
            <span class="small">{{ lang.wind }}</span>
          </div>

          <div class="table__card">
            <SvgVisibility></SvgVisibility>
            <span class="valeur">{{ file.visibility | toKm }} km</span>
            <span class="small">{{ lang.visibility }}</span>
          </div>

        </div>
      </div>
</template>

<script>
import SvgDrop from "@/components/svg/SvgDrop.vue";
import SvgWind from "@/components/svg/SvgWind.vue";
import SvgMinTemp from "@/components/svg/SvgMinTemp.vue";
import SvgMaxTemp from "@/components/svg/SvgMaxTemp.vue";
import SvgBarometer from "@/components/svg/SvgBarometer.vue";
import SvgVisibility from "@/components/svg/SvgVisibility.vue";

export default {
    name: 'Table',
    props: {
        file: {
            type: Object,
            default: function () {
            return { }
            }
        },
        lang: {
            type: Object,
            default: function () {
            return { }
            }
        }
    },
    filters: {
    toKm: function (value) {
      return value / 1000
    },
    toDate: function (timeStamp) {
      // var timeStamp = 1345902217, // le TimeStamp à convertir
      let date = new Date(timeStamp * 1000); // pour obtenir le timeStamp en millisecondes

      // let annee = date.getFullYear(); // on récupère l'année
      // let jour = date.getDate(); // on récupère le jour
      // let mois = date.getMonth(); // on récupère le nombre du mois (entre 0 et 11)
      let heure = date.getHours(); // on récupère l'heure
      let min = date.getMinutes(); // on récupère les minutes
      // let sec = date.getSeconds(); // on récupère les secondes
     
      // result = "le "+jour+"/"+mois+"/"+annee+" - "+heure+"h "+min+"min "+sec+"s"
      // console.log(result); // affichera : le 25/08/2012 - 15h 43min 37s
      return heure + ":" + min;
    },
  },
    components: {
        SvgDrop,
        SvgWind,
        SvgMinTemp,
        SvgMaxTemp,
        SvgBarometer,
        SvgVisibility,
    }
}
</script>


<style lang="scss" scoped>
.table__top {

    display: flex;
    flex-wrap: wrap;


    .table__card {
        width: 33.33%;
        margin-top: 15px;
        padding: 5px;
        text-align: center;

        .valeur {
            display: block;
            margin-top: 10px;
            // font-weight: 600;
        }

        .small {
            color: rgb(116, 116, 116);
            font-size: 0.8rem;
        }
    }
}
</style>