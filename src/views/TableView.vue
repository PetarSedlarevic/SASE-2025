<script lang="ts" setup>
import type { FlightModel } from '@/models/flight.model'
import { FlightService } from '@/services/flight.service'
import { formatTime } from '@/utils'
import { ref } from 'vue'

const flights = ref<FlightModel[]>()
FlightService.getFlights()
    .then(rsp => {
        flights.value = rsp.data
        flights.value = rsp.data
    })
</script>

<template>
    <table class="table table-striped table-hover" v-if="flights">
        <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Destination</th>
                <th scope="col">flight Number</th>
                <th scope="col">flight Key</th>
                <th scope="col">scheduled At</th>
                <th scope="col">Status</th>
                <th scope="col">Actions</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="f of flights" :key="f.id">
                <th scope="row">{{ f.id }}</th>
                <td>{{ f.destination }}</td>
                <td>{{ f.flightNumber }}</td>
                <td>{{ f.flightKey }}</td>
                <td>{{ formatTime(f.estimatedAt ?? f.scheduledAt) }}</td>
                <td>
                    <template v-if="f.estimatedAt">
                        <i class="fa-solid fa-circle text-warning"></i> Delayed
                    </template>
                    <template v-else>
                        <i class="fa-solid fa-circle text-success"></i> On time
                    </template>
                </td>
                <td>
                    <div class="card-body">
                        <RouterLink :to="`/flight/${f.id}`" class="btn btn-sm btn-primary">
                            <i class="fa-solid fa-arrow-up-right-from-square"></i> Details
                        </RouterLink>
                    </div>
                </td>
            </tr>
            <tr>
                <th scope="row">2</th>
                <td>Jacob</td>
                <td>Thornton</td>
                <td>@fat</td>
            </tr>
            <tr>
                <th scope="row">3</th>
                <td colspan="2">Larry the Bird</td>
                <td>@twitter</td>
            </tr>
        </tbody>
    </table>
</template>