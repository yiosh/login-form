<template>
  <v-app id="inspire">
    <v-app-bar
      height="50px"
      elevation="0"
      style="box-shadow: 0px 2px 5px 2px rgba(0, 0, 0, 0.1) !important;"
      app
      color="white"
      dark
    >
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
                <v-alert v-if="alertMessage" type="error">
                  {{ alertMessage }}
                </v-alert>
                <v-form>
                  <v-text-field
                    v-model="user"
                    placeholder="Username"
                    color="#ad1e24"
                    name="username"
                    prepend-icon="mdi-account"
                    type="text"
                  ></v-text-field>

                  <v-text-field
                    v-model="pwd"
                    id="password"
                    ref="password"
                    placeholder="Password"
                    color="#ad1e24"
                    name="password"
                    prepend-icon="mdi-lock"
                    type="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-layout justify-center wrap>
                  <v-flex style="text-align:center" xs12>
                    <v-btn
                      style="padding: 0 2em; margin: 0 auto;"
                      dark
                      color="#ad1e24"
                      :loading="loading"
                      @click="handleLogin"
                      >Login</v-btn
                    >
                    <!-- color="#d21919" -->
                  </v-flex>
                  <v-flex style="text-align:center; margin-top: 1em;" xs12>
                    <p>
                      Non sei registrato?
                      <a href="https://www.1x2live.it/" style="color: #ad1e24;"
                        >Registrati per accedere.</a
                      >
                    </p>
                  </v-flex>
                </v-layout>
                <!-- <v-spacer></v-spacer>
                
                <v-spacer></v-spacer> -->
              </v-card-actions>
            </v-card>
            <p style="text-align:center; margin-top: 2em;">
              2019 1x2live.it
            </p>
          </v-flex>
          <!-- <v-flex>
          </v-flex> -->
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    alertMessage: "",
    drawer: null,
    user: "",
    pwd: "",
    ip: "",
    loading: false,
    formData: new FormData()
  }),
  methods: {
    handleLogin() {
      this.formData.append("user", this.user);
      this.formData.append("pwd", this.pwd);
      this.formData.append("idh", this.ip);
      this.alertMessage = "";
      this.loading = true;

      axios
        .post(
          `${location.protocol}//${location.hostname}/fl_core/loginAjax.php`,
          this.formData,
          {
            headers: {
              "Content-Type": "multipart/form-data"
            }
          }
        )
        .then(response => {
          this.loading = false;
          console.log(response);

          if (response.data.redirect || response.data.includes("redirect")) {
            // window.location.href = response.data.redirect;
            window.location.href = location.origin;
          }

          if (response.data.esito != "OK") {
            this.alertMessage = response.data.esito;
          }
        })
        .catch(error => {
          this.loading = false;
          console.log(error);
        });
    }
  },
  created() {
    axios
      .get("https://json.geoiplookup.io")
      .then(response => {
        console.log("response", response.data);
        this.ip = response.data.ip;
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style>
#inspire {
  font-family: "Montserrat", sans-serif !important;
  background-color: rgb(245, 245, 245) !important;
}
</style>
