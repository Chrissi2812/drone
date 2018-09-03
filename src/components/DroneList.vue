<template>
    <div class="drone-list">
        <table>
            <thead>
            <td>Flugnummer</td>
            <td>Packete</td>
            <td>Streckenlänge</td>
            </thead>
            <tbody>
            <tr v-for="(drone) in drones" :key="drone.id">
                <td>{{drone.id}}</td>
                <td>{{drone.packages}}</td>
                <td>{{drone.routeLength}} Km</td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
  name: 'DroneList',
  data() {
    return {
      drones: [
        {
          id: 1,
          points: '',
          packages: 3,
          routeLength: 5.0,
        },
        {
          id: 2,
          points: '',
          packages: 10,
          routeLength: 15.2,
        },
      ],
    };
  },
};
</script>

<style scoped lang="scss">
    .drone-list {
        background: #69666d;
        color: #fff;
        table {
            border-spacing: 0;
            thead {
                background: rgba(#000, 0.2);
            }
            td {
                padding: .5em;
            }
        }
    }
</style>
