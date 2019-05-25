<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'app',
        components: {
            HelloWorld
        },
        created() {
            this.getLocation()
        },
        methods: {
            getLocation() {
                return new Promise((resolve, reject) => {
                    const geolocation = new BMap.Geolocation();

                    const map = new BMap.Map(document.createElement('div'));

                    // navigator.geolocation.getCurrentPosition(position => {
                    //     const ggPoint = new BMap.Point(position.coords.longitude, position.coords.latitude);
                    //     const convertor = new BMap.Convertor();
                    //     convertor.translate([ggPoint], 1, 5, data => {
                    //         if (data.status === 0) {
                    //             const bdPoint = data.points[0]
                    //
                    //             var myGeo = new BMap.Geocoder();
                    //             myGeo.getLocation(bdPoint, function(result){
                    //                 if (result){
                    //                     alert(result.address);
                    //                 }
                    //             });
                    //
                    //             // const map = new BMap.Map(document.createElement('div'));
                    //             //
                    //             // map.centerAndZoom(bdPoint, 19);
                    //             // const options = {
                    //             //     onSearchComplete: function (results) {
                    //             //         if (local.getStatus() === BMAP_STATUS_SUCCESS) {
                    //             //             return resolve(results.getPoi(0).title)
                    //             //         }
                    //             //     },
                    //             //     pageCapacity: 1 // 只取第一个结果
                    //             // };
                    //             // const local = new BMap.LocalSearch(map, options);
                    //             // local.search("医院");
                    //             // console.log(postion);
                    //         }
                    //     })
                    //
                    // },error => {
                    //     console.log(error);
                    // })

                    geolocation.getCurrentPosition(function (r) {
                        if (this.getStatus() === BMAP_STATUS_SUCCESS) {

                            const mPoint = new BMap.Point(r.point.lng, r.point.lat);

                            var myGeo = new BMap.Geocoder();
                            myGeo.getLocation(mPoint, function(result){
                                if (result){
                                    alert(result.address);
                                }
                            });
                            // map.centerAndZoom(mPoint, 19);
                            // const options = {
                            //     onSearchComplete: function (results) {
                            //         if (local.getStatus() === BMAP_STATUS_SUCCESS) {
                            //             for (var i = 0; i < results.getCurrentNumPois(); i++) {
                            //                 console.log(results.getPoi(i));
                            //                 // return resolve(results.getPoi(i).title)
                            //             }
                            //         }
                            //     },
                            //     pageCapacity: 10
                            // };
                            // const local = new BMap.LocalSearch(map, options);
                            // local.searchNearby('医院', mPoint, 1000);
                        } else {
                            reject('failed' + this.getStatus())
                        }
                    });
                })
            }
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
