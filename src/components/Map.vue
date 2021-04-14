<template>
    <div class="[ map ]">
        <!--        <div>-->
        <!--            <button class="m2 p1" @click="zoomCity(51.85, 19.13532, 6.8)">Polska</button>-->
        <!--            <button class="m2 p1" @click="zoomCity(51.107883, 17.038538, 13)">Wrocław</button>-->
        <!--            <button class="m2 p1" @click="zoomCity(	52.237049,	21.017532, 13)">Warszawa</button>-->
        <!--            <button class="m2 p1" @click="zoomCity(50.049683,	19.944544, 13)">Kraków</button>-->
        <!--        </div>-->
        <l-map
            v-if="showMap"
            :zoom="zoom"
            :center="center"
            :options="mapOptions"
            @update:center="centerUpdate"
            @update:zoom="zoomUpdate"
        >
            <l-tile-layer :url="url" :attribution="attribution"/>
<!--            <l-geo-json :geojson="geo" :options-style="styleFunction"/>-->

<!--                        <l-marker v-for="(pin, index) in currentPins" :lat-lng="[pin.latitude, pin.longitude]" :key="index">-->
<!--                            <l-icon :icon-url="icon" :icon-size="[50, 50]"></l-icon>-->
<!--                        </l-marker>-->
                        <l-marker v-for="(voivodeship, index) in voivodeships" :lat-lng="voivodeship.coords" :key="index">
                            <l-icon :icon-url="icon" :icon-size="[50, 50]">
                                <l-tooltip :options="{ permanent: true, interactive: true, direction: 'right', className: 'customTooltip' }">
                                    {{ (Math.ceil(Math.random() * 1000) + 200) }}
                                </l-tooltip>
                            </l-icon>
                        </l-marker>
<!--                        <l-marker v-for="(city, index) in cities" :lat-lng="city.coords" :key="index">-->
<!--                            <l-icon :icon-url="icon" :icon-size="[50, 50]"></l-icon>-->
<!--            &lt;!&ndash;                <l-tooltip :options="{ permanent: true, interactive: true }">&ndash;&gt;-->
<!--            &lt;!&ndash;                    <div @click="innerClick">&ndash;&gt;-->
<!--            &lt;!&ndash;                        I am a tooltip&ndash;&gt;-->
<!--            &lt;!&ndash;                        <p v-show="showParagraph">&ndash;&gt;-->
<!--            &lt;!&ndash;                            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque&ndash;&gt;-->
<!--            &lt;!&ndash;                            sed pretium nisl, ut sagittis sapien. Sed vel sollicitudin nisi.&ndash;&gt;-->
<!--            &lt;!&ndash;                            Donec finibus semper metus id malesuada.&ndash;&gt;-->
<!--            &lt;!&ndash;                        </p>&ndash;&gt;-->
<!--            &lt;!&ndash;                    </div>&ndash;&gt;-->
<!--            &lt;!&ndash;                </l-tooltip>&ndash;&gt;-->
<!--                        </l-marker>-->
        </l-map>
    </div>
</template>

<script>
import {latLng} from "leaflet";
import {LMap, LTileLayer, LMarker, LPopup, LTooltip, LIcon, LGeoJson} from "vue2-leaflet";
import pins from '../assets/pins.json';
import pin from '../assets/pin.png'

export default {
    name: "Map",
    components: { LMap, LTileLayer, LMarker, LPopup, LTooltip, LIcon, LGeoJson },
    data() {
        return {
            zoom: 6.9,
            center: latLng(52.15, 19.13532),
            url: 'https://tiles.stadiamaps.com/tiles/osm_bright/{z}/{x}/{y}{r}.png',
            attribution:
                '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
            currentZoom: 11.5,
            currentCenter: latLng(47.41322, -1.219482),
            showParagraph: false,
            mapOptions: {
                zoomSnap: 0.2,
                zoomControl: false
                // scrollWheelZoom: false,
                // icon: icon({
                //     iconUrl: "assets/pin.png",
                //     iconSize: [32, 37],
                //     iconAnchor: [16, 37]
                // }),
            },
            fillColor: "rgba(150,150,150,0.3)",
            icon: pin,
            // iconSize
            showMap: true,
            cities: [
                {coords: latLng(52.17, 19.13532)},
                {coords: latLng(52.37, 19.33532)},
                {coords: latLng(52.77, 19.73532)},
                {coords: latLng(52.97, 19.93532)},
            ],
            voivodeships: [
                {coords: latLng(53.57, 15.53)},
                {coords: latLng(54.15, 18.15)},
                {coords: latLng(53.85, 20.85)},
                {coords: latLng(53.20, 22.85)},
                {coords: latLng(52.17, 15.33)},
                {coords: latLng(52.27, 17.33)},
                {coords: latLng(53.10, 18.50)},
                {coords: latLng(52.40, 21.10)},
                {coords: latLng(51.20, 22.80)},
                {coords: latLng(51.10, 16.40)},
                {coords: latLng(51.60, 19.40)},
                {coords: latLng(50.80, 20.70)},
                {coords: latLng(50.65, 17.90)},
                {coords: latLng(50.55, 19.00)},
                {coords: latLng(49.85, 20.30)},
                {coords: latLng(49.85, 22.10)},
            ],
            currentPins: null,
            geo: null
        };
    },
    methods: {
        zoomUpdate(zoom) {
            this.currentZoom = zoom;
        },
        centerUpdate(center) {
            this.currentCenter = center;
        },
        showLongText() {
            this.showParagraph = !this.showParagraph;
        },
        innerClick() {
            this.$emit('openModal')
        },
        zoomCity(lat, lng, zoom) {
            this.center = latLng(lat, lng);
            // this.zoom = zoom;

            setTimeout(() => {
                this.center = latLng(lat, lng);
            }, 300)
        }
    },
    mounted() {
        this.currentPins = pins;

        fetch('https://raw.githubusercontent.com/ppatrzyk/polska-geojson/master/wojewodztwa/wojewodztwa-medium.geojson')
            .then(result => result.json())
            .then(result => this.geo = result);
    },
    computed: {
        styleFunction() {
            const fillColor = this.fillColor; // important! need touch fillColor in computed for re-calculate when change fillColor
            return () => {
                return {
                    weight: 2,
                    color: "#ECEFF1",
                    opacity: 1,
                    fillColor: fillColor,
                    fillOpacity: 1
                }
            }
        }
    }
};
</script>

<style lang="less">
.map {
    width: 100%;
    height: 100%;

    border-radius: 15px;
    overflow: hidden;
}

.customTooltip {
    margin-left: 10px!important;
    padding: 1px 2px 0!important;

    left: -8px!important;
    top: 25px!important;

    div {
        font-size: 11px!important;
    }

    &:before {
        content: none!important;
    }
}
</style>