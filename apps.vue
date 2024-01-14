<template>
  <NuxtLayout>
    <v-app>
      <v-container>
        <v-toolbar 
        class="py-1 px-4 bg-transparent"
        density="compact">
          <img style="width: 200px;" src="./public/logo.png" alt="wisata app">
        
          <v-spacer></v-spacer>
        
          <v-btn
            color="secondary"
            variant="flat"
          >
            The langham, jakarta . 25 - 25 Jan
          </v-btn>

          <v-spacer></v-spacer>

          <v-btn
            variant="flat"
            color="primary"   
          >
            Sign In
          </v-btn>
        </v-toolbar>
      </v-container>
      <main>
        <v-container>
          <div id="main__info" class="d-flex flex-row">
            <v-row>
              <v-col cols="4">
                <div class="d-flex align-center justify-center">
                  <v-avatar
                    class="ma-3"
                    size="180"
                    rounded="100"
                  >
                    <v-img src="https://cdn.vuetifyjs.com/images/cards/halcyon.png"></v-img>
                  </v-avatar>
                </div>
              </v-col>

              <v-col cols="8">
                <div>
                  <h3>The langham jakara</h3>
                  <div>
                    <p>Hotel</p>
                    <p>District 8 SCBD Lot 28, Jakarta, Indonesia</p>
                  </div>
                  <div class="d-flex justify-start align-center">
                    <v-progress-circular 
                      model-value="90"
                      color="purple"
                    >
                      90
                    </v-progress-circular>
                    <p class="ml-2">Excellent &middot; &nbsp;</p>
                    <p>17 Reviews</p>
                  </div>
                  <div>
                    <p>Business, romantic, city hotel with spa, shopping facilities in Jakarta (Senayan)</p>
                  </div>
                </div>
              </v-col>
            </v-row>

          </div>

          <div id="room__info">
            <v-row>
              <v-col
                cols="4"
              >
                <img style="width: 200px;" src="./public/logo.png" alt="wisata app">
              </v-col>
              <v-col
                cols="8"
              >
                <v-sheet
                  border="sm"
                  rounded="md"
                >
                  <div class="d-flex align-center justify-space-between">
                    <div>
                      <h3><v-icon end icon="mdi-bed-king-outline"></v-icon>Deluxe Room, 1 King Bed</h3>
                      <p><v-icon end icon="mdi-square-opacity"></v-icon>1 King Bed 42m</p>
                    </div>
                    <v-btn
                      color="primary"
                      variant="text"
                    >
                      See details
                    </v-btn>
                  </div>

                  <div v-for="i in 3">
                    <div class="d-flex align-center justify-space-between">
                      <div>
                        <p>Without Breakfast</p>
                        <p>Non-Refundable</p>
                      </div>
                      <div>
                        ds
                      </div>
                    </div>

                    <div>
                      <v-row>
                        <v-col cols="10">
                          <p>
                            Save 25% Today
                          </p>
                          <p>
                            Rp 6,567,765
                          </p>
                          <p>
                            Rp 6,567,765
                          </p>
                          <p>After tax & fees</p>
                          <p>Member-only price, valid in app only</p>
                        </v-col>
                        <v-col cols="2">
                          <v-btn>Book Now</v-btn>
                          <p>Collect 3 Points</p>
                        </v-col>
                      </v-row>
                    </div>
                  </div>
                </v-sheet>
              </v-col>
            </v-row>
          </div>
        </v-container>
      </main>
      <footer></footer>
    </v-app>
  </NuxtLayout>
</template>