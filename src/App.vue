<template>
  <v-app id="inspire">
    <v-app-bar height="50px" elevation="0" style="box-shadow: 0px 2px 5px 2px rgba(0, 0, 0, 0.1) !important;" app color="white" dark>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <!-- <v-btn href="https://pcmax-web.it/fersino/chi-siamo/" light icon>
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn> -->

      <!-- <v-spacer></v-spacer> -->
      <v-img
        src="https://secure.1x2live.it/fl_config/secure.1x2live.it/img/logo.jpg"
        max-height="100%"
        contain
      ></v-img>
    </v-app-bar>

    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center wrap>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-2">
              <v-toolbar dark color="black" flat>
                <v-toolbar-title>Login</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    label="Username"
                    name="username"
                    prepend-icon="mdi-account"
                    type="text"
                  ></v-text-field>

                  <v-text-field
                    id="password"
                    label="Password"
                    name="password"
                    prepend-icon="mdi-lock"
                    type="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-layout justify-center wrap>
                  <v-flex style="text-align:center" xs12>
                    <v-btn style="padding: 0 2em; margin: 0 auto;" dark color="#d21919">Login</v-btn>
                  </v-flex>
                  <v-flex style="text-align:center; margin-top: 1em;" xs12>
                    <p>Non sei registrato? <a href="//demo.condivision.cloud/v4/fl_app/registerForm">Registrati per accedere.</a></p>
                  </v-flex>
                </v-layout>
                <!-- <v-spacer></v-spacer>
                
                <v-spacer></v-spacer> -->
              </v-card-actions>
            </v-card>
            <p style="text-align:center; margin-top: 2em;">2019 1x2live.it – <a href="//pcmax-web.it/fersino/chi-siamo/">Torna al sito web</a></p>
          </v-flex>
          <!-- <v-flex>
          </v-flex> -->
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  // props: {
  //   source: String
  // },
  data: () => ({
    drawer: null
  })
};
</script>

<style>
#inspire {
  font-family: "Montserrat", sans-serif !important;
  background-color: #f5f5f5;
}
</style>

