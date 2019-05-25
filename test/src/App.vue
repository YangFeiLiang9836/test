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
                    navigator.geolocation.getCurrentPosition(position => {
                        const ggPoint = new BMap.Point(position.coords.longitude, position.coords.latitude);
                        const convertor = new BMap.Convertor();
                        convertor.translate([ggPoint], 1, 5, data => {
                            if (data.status === 0) {
                                const bdPoint = data.points[0]

                                const map = new BMap.Map(document.createElement('div'));

                                map.centerAndZoom(bdPoint, 19);
                                const options = {
                                    onSearchComplete: function (results) {
                                        if (local.getStatus() === BMAP_STATUS_SUCCESS) {
                                            alert(results.getPoi(0).title)
                                            return resolve(results.getPoi(0).title)
                                        }
                                    },
                                    pageCapacity: 1 // 只取第一个结果
                                };
                                const local = new BMap.LocalSearch(map, options);
                                local.search("医院");
                            }
                        })

                    }, error => {
                        reject()
                    })
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
