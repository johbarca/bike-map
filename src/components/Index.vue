<template>
    <div class="hello">
        <div style="height:800px" id="container" tabindex="0"></div>
    </div>
</template>

<script>
import AMap from "AMap";
export default {
    name: "Index",
    data() {
        return {
            pointList: [
                {
                    lng: 116.397428,
                    lat: 39.90923
                },
                {
                    lng: 116.397428,
                    lat: 39.90923
                },
                {
                    lng: 116.397428,
                    lat: 39.90923
                },
                {
                    lng: 116.397428,
                    lat: 39.90923
                }
            ]
        };
    },
    mounted() {
        this.init();
    },
    methods: {
        init: function() {
            let map = new AMap.Map("container", {
                mapStyle: "amap://styles/b9860bb75788fd64ad29e2de67e8be28",
                center: [121.47, 31.23]
                /* resizeEnable: true,
                zoom: 10,
                lang: "en" */
            });
            /* AMap.plugin(["AMap.ToolBar", "AMap.Scale"], function() {
                map.addControl(new AMap.ToolBar());
                map.addControl(new AMap.Scale());
            }); */
            this.completeEventHandler();
        },
        completeEventHandler(x, y) {
            marker3 = new AMap.Marker({
                map: map,
                //draggable:true, //是否可拖动
                position: new AMap.LngLat(x, y), //基点位置
                icon: "http://code.mapabc.com/images/car_03.png", //marker图标，直接传递地址url
                offset: new AMap.Pixel(-26, -13), //相对于基点的位置
                autoRotation: true
            });
            var lngX;
            var latY;
            lineArr = new Array();
            let pointList = this.pointList;
            for (var i = 1; i < pointList.length; i++) {
                lngX = pointList[i].lng;
                latY = pointList[i].lat;
                lineArr.push(new AMap.LngLat(lngX, latY));
            }

            //绘制轨迹
            var polyline = new AMap.Polyline({
                map: map,
                path: lineArr,
                strokeColor: "#00A", //线颜色
                strokeOpacity: 1, //线透明度
                strokeWeight: 3, //线宽
                strokeStyle: "solid" //线样式
            });
        },
        startRun() {
            //开始绘制轨迹
            x = pointList[0].lng;
            y = pointList[0].lat;
            completeEventHandler(x, y);
            marker.moveAlong(lineArr, 80); //开始轨迹回放
        }
    }
};
</script>
