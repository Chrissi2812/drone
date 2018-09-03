<template>
    <div id="map" class="map">
        <button @click="addNewRoute" class="mdc-fab mdc-fab--extended">
            <span class="material-icons mdc-fab__icon">add</span>
            <span class="mdc-fab__label">Neue Route</span>
        </button>
    </div>
</template>

<script>
import 'ol/ol.css';
import Map from 'ol/Map';
import View from 'ol/View';
import { transform as OlTransform } from 'ol/proj';
import Draw from 'ol/interaction/Draw';
import { Tile as TileLayer, Vector as VectorLayer } from 'ol/layer';
import { OSM, Vector as VectorSource } from 'ol/source';


export default {
  name: 'Map',
  data() {
    return {
      zoom: 11,
      center: [7.576667, 53.674167],
      rotation: 0,
      map: null,
    };
  },
  methods: {
    addNewRoute() {
      // eslint-disable-next-line no-underscore-dangle
      this.draw.startDrawing_({ coordinate: this.transformCoordinates(this.center) });
      this.map.addInteraction(this.draw);
      this.draw.addEventListener('drawend', (event) => {
        console.log(event);
        this.map.removeInteraction(this.draw);
      });
    },
    transformCoordinates(coordinates) {
      return OlTransform(coordinates, 'EPSG:4326', 'EPSG:3857');
    },
  },
  mounted() {
    const raster = new TileLayer({
      source: new OSM(),
    });
    this.source = new VectorSource({
      wrapX: false,
    });
    const vector = new VectorLayer({
      source: this.source,
    });
    this.map = new Map({
      layers: [raster, vector],
      target: 'map',
      view: new View({
        projection: 'EPSG:3857',
        center: this.transformCoordinates(this.center),
        zoom: this.zoom,
      }),
    });

    this.draw = new Draw({
      source: this.source,
      type: 'LineString',
    });
  },
};
</script>

<style scoped lang="scss">
    @import "@material/fab/mdc-fab";

    .map {
        position: relative;
        height: 100%;
        width: 100%;
        .ol-viewport {
            position: absolute!important;
        }
    }
    .mdc-fab {
        position: absolute;
        z-index: 1;
        bottom: 1em;
        right: 1em;
    }
</style>
