<template>
    <div class="wrapper__sun">
        <div class="left">
          <span>{{ (file.sys.sunrise + ( file.timezone -1000 )) | toDateHM }}</span>
          <small class="small">{{ lang.sunrise }}</small>
        </div>

        <div class="center">
            <span>{{ (file.dt + ( file.timezone )) | toDateHM }}</span>
            <div class="wrapper__dessin">
                <div class="dessin">
                    <span class="sunSpan" :class="{ jour : isJour, nuit : isNuit }" :style="{ left : positionCercle + '%' } "></span>
                </div>
            </div>
        </div>

        <div class="right">
          <span>{{ (file.sys.sunset + ( file.timezone  )) | toDateHM }}</span>
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
    computed: {
        positionCercle() {
            let deb = this.hourRound(this.file.sys.sunrise + ( this.file.timezone  ))
            let act = this.hourRound(this.file.dt + ( this.file.timezone  ))
            let fin = this.hourRound(this.file.sys.sunset +( this.file.timezone  ))
            
            let result = act * 100 / ( deb + fin )

            console.log(result)
            return result

        },
        isJour() {
            let deb = this.file.sys.sunrise
            let act = this.file.dt
            let fin = this.file.sys.sunset
            if ( deb <= act && act <= fin) {
                // console.log('jour')
                return true
            } else {
                // console.log('nuit')
                return false
            }
        },
        isNuit() {
            let deb = this.file.sys.sunrise
            let act = this.file.dt
            let fin = this.file.sys.sunset
            if ( deb <= act && act <= fin) {
                console.log('jour')
                return false
            } else {
                console.log('nuit')
                return true
            }
        }
    }, 
    methods: {
        hourRound(timestamp) {
            let date = new Date(timestamp * 1000);
            let heure = date.getUTCHours();
            return Math.round(heure)
        },
    },
    filters: {
        toDateHM: function (timeStamp) {
        
        let date = new Date(timeStamp * 1000); 
        let heure = date.getUTCHours();
        let min = date.getUTCMinutes();
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
        margin-top: 5px;
        width: 100%;
        height: 1px;
        background: rgb(116, 116, 116);
       
   
        .sunSpan {
            position: absolute;
            bottom: calc(0% - 10px);
            // right: calc(50% - 10px);
            width: 20px;
            height: 20px;
            border-radius: 50%;
            // border: 1px solid red;
        }

        .jour {
            background: rgb(231, 111, 31);
            border: 1px solid rgb(231, 111, 31);
        }

        .nuit {
            background: rgb(46, 46, 189);
            border: 1px solid rgb(46, 46, 189);
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
        margin-top: 5px;
        display: block;
        color: rgb(116, 116, 116);
        font-size: 0.8rem;
    }
}

</style>