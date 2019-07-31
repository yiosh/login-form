<template>
  <v-app id="inspire">
    <v-app-bar app color="white" dark>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-btn href="https://pcmax-web.it/fersino/chi-siamo/" light icon>
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>

      <!-- <v-spacer></v-spacer> -->
      <v-img
        src="https://secure.1x2live.it/fl_config/secure.1x2live.it/img/logo.jpg"
        max-height="100%"
        contain
      ></v-img>
    </v-app-bar>

    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="#d21919" flat>
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
                <v-spacer></v-spacer>
                <v-btn style="padding: 0 2em" dark color="#d21919">Login</v-btn>
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-flex>
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

