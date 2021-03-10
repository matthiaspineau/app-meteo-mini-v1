<template>
    <div class="wrapper__sun">
        <div class="left">
          <span>{{ file.sys.sunrise | toDate }}</span>
          <small class="small">{{ lang.sunrise }}</small>
        </div>
        <div class="center">
            <div class="wrapper__dessin">
                <div class="dessin">

                </div>
            </div>
            <span>{{ file.dt | toDate }}</span>
        </div>
        <div class="right">
          <span>{{ file.sys.sunset | toDate }}</span>
          <small class="small">{{ lang.sunset }}</small>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Sun',
    props: {
        file: {
            type: Object,
            default: function () {
                return {}
            }
        },
        lang: {
            type: Object,
            default: function () {
                return {}
            }
        }
    },
    filters: {
        toDate: function (timeStamp) {
        
        let date = new Date(timeStamp * 1000); 
        let heure = date.getHours();
        let min = date.getMinutes();
        return heure + ":" + min;
        },
    }
}
</script>

<style lang="scss" scoped>


// .wrapper__dessin {
//     // position: relative;
//     margin: 0 auto;

//     .dessin {
//         position: relative;

//         width: 150px;
//         height: 80px;

//         border-radius: 50%;
//          border-radius: 50%/80px 80px 0 0;
//         border: 1px solid #fff;

//         &::before {
//             content: '';
//             position: absolute;
//             bottom: calc(0% - 10px);
//             left: calc(0% - 10px);
//             width: 20px;
//             height: 20px;
//             border-radius: 50%;
//             border: 1px solid blue;
//         }

//         &::after {
//             content: '';
//             position: absolute;
//             bottom: calc(100% - 10px);
//             right: calc(50% - 10px);
//             width: 20px;
//             height: 20px;
//             border-radius: 50%;
//             border: 1px solid red;
//         }
//     }
// }


.wrapper__sun {
    display: flex;
    align-items: baseline;

    .center {
        width: 50%;
        padding: 5px;
        text-align: center;
    }
    .left, .right {
        width: 25%;
        padding: 5px;
        text-align: center;

        span {
            display: block;
        }
    }

    .small {
        color: rgb(116, 116, 116);
        font-size: 0.8rem;
    }
}

</style>