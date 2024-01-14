<template>
    <v-container class="container">
        <div class="pa-lg-8 py-10">
            <div id="main__info" class="d-flex flex-row pa-lg-6 py-4">
                <v-row class="py-lg-2">
                    <v-col lg="4">
                        <div class="d-flex align-center justify-center">
                            <v-avatar size="180" rounded="100">
                                <v-img :src="property.catalog.hero_image_url.lg" :aspect-ratio="1" cover></v-img>
                            </v-avatar>
                        </div>
                    </v-col>

                    <v-col lg="8">
                        <div v-if="propertyPending">
                            <v-skeleton-loader color="secondary" type="article"></v-skeleton-loader>
                        </div>
                        <div v-else>

                            <h3>{{ property.name }}</h3>
                            <div class="text-body-2">
                                <p class="py-1 text-capitalize text-grey-darken-1">{{ property.type }}</p>
                                <p>{{ property.catalog.address_full }}</p>
                            </div>
                            <div class="d-flex justify-start align-center py-2 text-body-2">
                                <v-progress-circular 
                                    :model-value="property.catalog.review_rating" 
                                    :color="ratingDesc(property.catalog.review_rating).color"
                                >
                                    {{ property.catalog.review_rating }}
                                </v-progress-circular>
                                <p class="ml-2">{{ ratingDesc(property.catalog.review_rating).text }} &middot; &nbsp;</p>
                                <p>{{ property.catalog.review_count }} Reviews</p>
                            </div>
                            <div class="py-1 text-body-2">
                                <p>Business, romantic, city hotel with spa, shopping facilities in Jakarta (Senayan)</p>
                            </div>
                        </div>
                    </v-col>
                </v-row>
            </div>

            <div v-if="availabilityPending">
                Loading....
            </div>
            <div v-else>
                <div class="py-2 pa-lg-4 ga-2 d-flex flex-column flex-lg-row justify-lg-center">
                    <div>
                        <v-icon size="x-small" icon="mdi-filter-outline"></v-icon>
                        <span class="text-body-2 font-weight-medium">Filter rooms by</span>
                    </div>
                    <div class="d-flex flex-row ga-2">
                        <v-btn 
                            @click="filters.free_breakfast=!filters.free_breakfast"
                            :color="filters.free_breakfast === true ? 'blue' : ''"
                            class="text-none"
                            variant="outlined"
                            rounded="xl"
                            size="small"
                            prepend-icon="mdi-silverware-fork-knife"
                        >Free Breakfast</v-btn>
                        <v-btn 
                            @click="filters.free_cancellation=!filters.free_cancellation"
                            :color="filters.free_cancellation === true ? 'blue' : ''"
                            class="text-none"
                            variant="outlined" 
                            rounded="xl"
                            size="small"
                            prepend-icon="mdi-credit-card-check"
                        >Free Cancellation</v-btn>
                    </div>
                </div>

                <v-row class="rooms-offer my-4 my-lg-6" :no-gutters="true" v-for="room in property.room">
                    <v-col class="room-images px-md-4">
                        <v-img v-if="room.images.length < 1" :src="fallbackRoomImageUrl" class="bg-grey-lighten-2">
                            <template v-slot:placeholder>
                                <v-row class="fill-height ma-0" align="center" justify="center">
                                    <v-progress-circular indeterminate color="grey-lighten-5"></v-progress-circular>
                                </v-row>
                            </template>
                        </v-img>
                        <v-img v-if="room.images.length < 3" :src="room.images[0]" class="bg-grey-lighten-2">
                            <template v-slot:placeholder>
                                <v-row class="fill-height ma-0" align="center" justify="center">
                                    <v-progress-circular indeterminate color="grey-lighten-5"></v-progress-circular>
                                </v-row>
                            </template>
                        </v-img>
                        <div class="images-grid" v-else>
                            <div v-for="(image, index) in room.images.slice(0, 4)" :key="n"
                                :class="`${index === 0 ? 'parent' : 'children-' + index}`">
                                <img class="" :src="Object.values(image.links)[2].href"
                                    style="width: 100%; height: 100%; object-fit: cover;" />
                            </div>
                        </div>
                    </v-col>
                    <v-col class="room-detail">
                        <v-sheet border="sm" class="rounded-top room-detail">
                            <div class="d-flex align-center justify-space-between">
                                <div class="pa-4">
                                    <span class="font-weight-medium text-h6">{{ room.name }}</span>
                                    <div class="d-flex flex-row ga-2 align-center">
                                        <div v-if="room.bed_groups">
                                            <v-icon size="x-small" icon="mdi-bed-king-outline"></v-icon>
                                            <span class="pl-2">{{ Object.values(room.bed_groups)[0].description }}</span>
                                        </div>
                                        <div v-if="room.area">
                                            <v-icon size="x-small" icon="mdi-square-opacity"></v-icon>
                                            <span class="pl-2">{{ room.area.square_meters }} m<sup>2</sup> </span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </v-sheet>
                    </v-col>

                    <v-col class="room-availability">
                        <v-sheet border="sm" class="rounded-bottom">
                            <div v-for="(offer, index) in rooms.filter(item => item.room_data.id == room.id)" v-if="rooms.filter(item => item.room_data.id == room.id).length > 0">
                                <AvailabilityRoom :offer="offer" />
                            </div>
                            <div v-else>
                                <NoRoomAvailable/>
                            </div>
                        </v-sheet>
                    </v-col>
                </v-row>
            </div>
        </div>
    </v-container>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const ratingDesc = (score) => {
    if(score < 50) 
        return {
            color: 'red',
            text: 'Bad'
        }
    else if(score < 80)
        return {
            color: 'blue',
            text: 'So so'
        }
    else {
        return {
            color: 'purple',
            text: 'Awesome'
        }
    }
}

let filters = reactive({
    free_breakfast: null,
    free_cancellation: null
})

const fallbackRoomImageUrl = ref('https://wisata.app/img/fallback-room.png')

const route = useRoute()
const slug = route.params.slug
const propertyId = slug.split('-').at('-1')

const checkinDate = route.query.checkin
const checkoutDate = route.query.checkout
const guestPerRoom = route.query.guest_per_room
const numberOfRoom = route.query.number_of_room



const propertyUrl = `https://exterior-technical-test-api.vercel.app/property?id=${propertyId}&include=room`
const { propertyPending, data: property } = useFetch(propertyUrl, {
    lazy: true,
    transform(data) {
        return data[Object.keys(data)[0]]
    }
})

const availabilityUrl = `https://exterior-technical-test-api.vercel.app/property/availability/${propertyId}?checkin=${checkinDate}&checkout=${checkoutDate}&number_of_room=${numberOfRoom}&guest_per_room=${guestPerRoom}`

const { availabilityPending, data: rooms } = useFetch(availabilityUrl, {
    lazy: true,
    transform(data) {
        console.log(data.offer_list.filter(item => item.room_data.id == "219929639"));
        return data.offer_list
    }
})
</script>

<style>
.rounded-top {
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

.rounded-bottom {
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
}

.rooms-offer {
    display: grid;
    grid-template-areas: "room-detail" "room-images" "room-availability";
}

@media (min-width: 600px) {
    .rooms-offer {
        grid-template:
            "room-images room-detail room-detail" min-content
            "room-images room-availability room-availability" 1fr
            / minmax(auto, 250px) minmax(250px, 1fr) minmax(auto, 250px);
    }

    .images-grid {
        border-radius: 10px;
    }
}

.images-grid {
    overflow: hidden;
    display: grid;
    grid-gap: 5px;
    grid-template-areas:
        "parent parent parent"
        "children-1 children-2 children-3";
}


.parent {
    grid-area: parent;
}

.children-1 {
    grid-area: children-1;
}

.children-2 {
    grid-area: children-2;
}

.children-3 {
    grid-area: children-3;
}

.room-detail {
    border-bottom: none !important;
    grid-area: room-detail;
}

.room-images {
    grid-area: room-images;
}

.room-availability {
    grid-area: room-availability;
}
</style>