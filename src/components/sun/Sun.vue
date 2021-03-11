<template>
    <div class="wrapper__sun">
        <div class="left">
          <span>{{ file.sys.sunrise | toDateHM }}</span>
          <small class="small">{{ lang.sunrise }}</small>
        </div>
        <div class="center">
            <div class="wrapper__dessin">
                <div class="dessin">
                    <span class="sunSpan"></span>
                </div>
            </div>
            <span>{{ file.dt | toDateHM }}</span>
        </div>
        <div class="right">
          <span>{{ file.sys.sunset | toDateHM }}</span>
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
    // methods: {
    //     calcul() {
    //         obj.dt*1000-(obj.timezone*1000)
    //     }
    // },
    filters: {
        toDateHM: function (timeStamp) {
        
        let date = new Date(timeStamp * 1000); 
        let heure = date.getHours();
        let min = date.getMinutes();
        heure = heure.toString().length > 1 ? heure.toString() : '0' + heure
        min = min.toString().length > 1 ? min.toString() : '0' + min
        return heure + ":" + min;
        },
    }
}
</script>

<style lang="scss" scoped>


.wrapper__dessin {
    // position: relative;
    margin: 0 auto;
    padding-bottom: 10px;
    padding-top: 10px;

    .dessin {
        position: relative;

        width: 100%;
        height: 1px;
        background: #fff;
       
   
        .sunSpan {
            position: absolute;
            bottom: calc(0% - 10px);
            right: calc(50% - 10px);
            width: 20px;
            height: 20px;
            border-radius: 50%;
            border: 1px solid red;
        }
        
    }
}


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