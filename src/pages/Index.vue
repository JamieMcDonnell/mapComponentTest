<template>
  <q-page class="row items-center justify-evenly">
    Google Maps Test
    <q-btn class="bg-white" label="Toggle Fields" @click="hideField" />
    <div style="width: 500px; height: 500px; display: block;">
      <google-map
        :api-key="gmapsKey"
        style="width: 100%; height: 500px"
        :center="center"
        :zoom="15"
        mapTypeId="satellite"
        ref="newMap"
        key="dupeMap"
      >
        <Polygon
          v-for="polygon in polygons"
          :options="polygon"
          :key="polygon.id"
          :ref="el => { if (el) polygonRefs[polygon.id] = el }"
          @click="polyClick($event, polygon)"
        />
      </google-map>
    </div>
  </q-page>
</template>

<script lang="ts">
interface Base {
  id: number;
  created: null | number;
  lastModified: null | number;
  [key: string]: unknown
}
interface NewEntity extends Base {
  newEntity: boolean;
}
interface SimpleFieldCrop extends NewEntity {
  boundaryId: number | string;
  cropTypeColor: string;
  cropTypeId: number;
  cropTypeName: string;
  fieldId: number | string;
}
interface BoundaryMapPoint {
  poly: number;
  type: string;
  ring: number;
  seq: number;
  lat: number;
  lon: number;
}
interface BoundaryType extends NewEntity {
  precedence: number;
  priorityForFieldAnaylticsSort: number;
}
interface BoundaryMapBoundary {
  fieldCrop?: SimpleFieldCrop;
  boundaryId: number | string;
  boundaryName: string;
  boundaryAcres: number;
  boundaryMapPoints: BoundaryMapPoint[];
  boundaryType?: BoundaryType;
}
interface Boundary {
  fieldId: number | string;
  fieldName: string;
  boundaryMapBoundary: {
    [key: number]: BoundaryMapBoundary;
    [key: string]: BoundaryMapBoundary;
  };
  fillColor?: string;
  strokeColor?: string;
  strokeWeight?: number;
  zIndex?: number;
  preventZoom?: boolean;
}
import { defineComponent, ref, Ref, computed, onBeforeUpdate } from 'vue'
import { GoogleMap, Polygon } from 'vue3-google-map'
import { uid } from 'quasar'

export default defineComponent({
  name: 'Reporting',
  components: { /* Gmap, */GoogleMap, Polygon },
  setup () {
    const defaultLat = 38.46834221398079
    const defaultLng = -100.80901789702166
    const google = ref()

    const fields: Boundary[] = [
    {
      fieldId: 1,
      fieldName: 'Field #1',
      boundaryMapBoundary: {
        2: {
          boundaryId: 2,
          boundaryName: 'Field - CLU',
          boundaryType: {
            id: 1,
            created: 1607049693382,
            lastModified: 1607049693382,
            name: 'Field Boundary',
            precedence: 1,
            priorityForFieldAnaylticsSort: 0,
            newEntity: false
          },
          boundaryAcres: 161.91,
          boundaryMapPoints: [
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 0,
              lat: 38.46834221398079,
              lon: -100.80901789702166
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 1,
              lat: 38.468360446952005,
              lon: -100.8051972567932
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 2,
              lat: 38.468360446952005,
              lon: -100.8051972567932
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 3,
              lat: 38.467599741286534,
              lon: -100.8052207520801
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 4,
              lat: 38.465830024010636,
              lon: -100.80526151568708
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 5,
              lat: 38.464080470071764,
              lon: -100.80529430054803
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 6,
              lat: 38.462331682433934,
              lon: -100.80527617236964
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 7,
              lat: 38.46115071078435,
              lon: -100.80528112035144
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 8,
              lat: 38.461004954636024,
              lon: -100.80528173812431
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 9,
              lat: 38.46097733934402,
              lon: -100.80810819444878
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 10,
              lat: 38.46095462521989,
              lon: -100.81401700378036
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 11,
              lat: 38.46096835040433,
              lon: -100.81442471728141
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 12,
              lat: 38.46103546652606,
              lon: -100.81442581467473
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 13,
              lat: 38.461469189524365,
              lon: -100.8144329245082
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 14,
              lat: 38.4634182880594,
              lon: -100.81444781196772
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 15,
              lat: 38.465367780538934,
              lon: -100.81443723358416
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 16,
              lat: 38.4673102121541,
              lon: -100.81445195906657
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 17,
              lat: 38.46833148043674,
              lon: -100.81445901298488
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 18,
              lat: 38.46834221398079,
              lon: -100.80901789702166
            }
          ]
        }
      }
    },
    {
      fieldId: 2,
      fieldName: 'Field #2',
      boundaryMapBoundary: {
        6: {
          boundaryId: 6,
          boundaryName: 'Field - CLU',
          boundaryType: {
            id: 1,
            created: 1607049693382,
            lastModified: 1607049693382,
            name: 'Field Boundary',
            precedence: 1,
            priorityForFieldAnaylticsSort: 0,
            newEntity: false
          },
          boundaryAcres: 481.21,
          boundaryMapPoints: [
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 0,
              lat: 38.468137704675065,
              lon: -100.85639415578453
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 1,
              lat: 38.4681243406058,
              lon: -100.85428796916578
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 2,
              lat: 38.46813943862307,
              lon: -100.85291277374752
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 3,
              lat: 38.46815863620713,
              lon: -100.851699018081
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 4,
              lat: 38.46815275789018,
              lon: -100.8516479201969
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 5,
              lat: 38.468106591121824,
              lon: -100.85161276660757
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 6,
              lat: 38.46801343400067,
              lon: -100.85159340883672
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 7,
              lat: 38.46625814252516,
              lon: -100.85156548571473
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 8,
              lat: 38.464382226092376,
              lon: -100.8515684515328
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 9,
              lat: 38.46249361286442,
              lon: -100.85152864345132
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 10,
              lat: 38.460923596971384,
              lon: -100.85152468676378
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 11,
              lat: 38.460651175136015,
              lon: -100.85152397789818
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 12,
              lat: 38.45871545414108,
              lon: -100.85150846011972
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 13,
              lat: 38.456859934553634,
              lon: -100.85148648111269
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 14,
              lat: 38.454971077500105,
              lon: -100.85146366434327
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 15,
              lat: 38.45376325497449,
              lon: -100.85143278640744
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 16,
              lat: 38.45369611635692,
              lon: -100.85145652154192
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 17,
              lat: 38.453641924112674,
              lon: -100.85150607344075
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 18,
              lat: 38.45362776993652,
              lon: -100.85155666032956
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 19,
              lat: 38.45363037605279,
              lon: -100.85519026762348
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 20,
              lat: 38.45361773379471,
              lon: -100.85893382508765
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 21,
              lat: 38.453618473236006,
              lon: -100.86070718130107
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 22,
              lat: 38.453618473236006,
              lon: -100.86070718130107
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 23,
              lat: 38.455839072449926,
              lon: -100.86068904885195
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 24,
              lat: 38.45584625501486,
              lon: -100.86068900420501
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 25,
              lat: 38.45604695875367,
              lon: -100.86069585716986
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 26,
              lat: 38.45731985358981,
              lon: -100.86073931384698
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 27,
              lat: 38.460870375955295,
              lon: -100.86086054874801
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 28,
              lat: 38.46085845187328,
              lon: -100.86412905331413
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 29,
              lat: 38.4608842283555,
              lon: -100.86995991010909
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 30,
              lat: 38.460905508264176,
              lon: -100.86996130778444
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 31,
              lat: 38.46095235303285,
              lon: -100.86996437425377
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 32,
              lat: 38.46234740817949,
              lon: -100.86997491665417
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 33,
              lat: 38.46375580237246,
              lon: -100.86998583950167
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 34,
              lat: 38.46529740573922,
              lon: -100.87001716757447
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 35,
              lat: 38.465858205582,
              lon: -100.87001466844171
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 36,
              lat: 38.468053869856305,
              lon: -100.87005440407545
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 37,
              lat: 38.46810153964839,
              lon: -100.86999620658754
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 38,
              lat: 38.46811637915409,
              lon: -100.86990319982256
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 39,
              lat: 38.4681230156928,
              lon: -100.8665578189838
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 40,
              lat: 38.46813565108295,
              lon: -100.86283046762182
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 41,
              lat: 38.468126687659044,
              lon: -100.85961206722628
            },
            {
              poly: 0,
              type: 'E',
              ring: 0,
              seq: 42,
              lat: 38.468137704675065,
              lon: -100.85639415578453
            }
          ]
        }
      }
    }
  ]

  interface PolygonOptions {
    paths: { lat: number; lng: number; }[];
    strokeColor: string;
    strokeOpacity: number;
    strokeWeight: number;
    fillColor: string;
    fillOpacity: number;
    id: number;
    uid: string;
  }

  const polygons = computed(() => {
    const polygons: PolygonOptions[] = []

    fields.forEach(field => {
      Object.keys(field.boundaryMapBoundary).forEach(key => {
        const boundary = field.boundaryMapBoundary[key]
        polygons.push(
        {
          paths: boundary.boundaryMapPoints.map(point => {
            return { lat: point.lat, lng: point.lon }
          }),
          strokeColor: '#FF0000',
          strokeOpacity: 0.8,
          strokeWeight: 2,
          fillColor: '#FF0000',
          fillOpacity: 0.35,
          id: boundary.boundaryId as number,
          uid: uid()
        }
      )
      })
    })

    return polygons
  })

    const state = ref(false)
    const hideField = () => {
      if (polygonRefs.value) {
        for (const id in polygonRefs.value) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment
          // @ts-ignore
          const polygon = polygonRefs.value[+id].polygon.component.value as google.maps.Polygon

          if (newMap.value && newMap.value.map) {
            if (state.value) {
              polygon.setMap(newMap.value.map)
              polygon.setVisible(true)
            } else {
              polygon.setMap(null)
              polygon.setVisible(false)
            }
          }
        }
        state.value = !state.value
      }
    }

    // const gmapsKey = process.env.gmapsKey
    const gmapsKey = 'AIzaSyAIQ3Il5YcF0Quew7EWpx6BwqRix9zXIGM'
    const center = { lat: defaultLat, lng: defaultLng }
    const newMap = ref<typeof GoogleMap | null>(null)
    interface PolygonRefs {
      [key: number]: {
        options: PolygonOptions,
        polygon: {
          component: Ref<google.maps.Polygon>
        }
      }
    }

    const polygonRefs = ref<PolygonRefs>({})
    // make sure to reset the refs before each update
    onBeforeUpdate(() => {
      polygonRefs.value = {}
    })

    const polyClick = (ev: unknown, polygon: PolygonOptions) => {
      console.log('polyClick: ', ev, polygon)
      console.log('Poly Map: ', polygonRefs.value[polygon.id].polygon.component.getMap())
    }

    return {
      google,
      hideField,
      gmapsKey,
      center,
      polygons,
      newMap,
      polygonRefs,
      polyClick
    }
  }
})
</script>
