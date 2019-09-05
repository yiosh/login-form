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
      <v-img
        src="https://demo.condivision.cloud/fl_config/demo.condivision.cloud/img/logo.png"
        max-height="100%"
        contain
      ></v-img>
    </v-app-bar>

    <v-content>
      <v-container fill-height>
        <v-row>
          <v-col cols="3">
            <v-card class="elevation-2">
              <v-toolbar dark color="#454545" flat>
                <v-toolbar-title>Login</v-toolbar-title>
              </v-toolbar>
              <!-- <v-card-text> -->
              <v-container>
                <v-row justify="center">
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
                </v-row>
              </v-container>
              <!-- </v-card-text> -->
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
                  <v-flex
                    style="text-align:center; margin-top: 1em; font-size:small;"
                    xs12
                  >
                    <p>
                      Non sei registrato?
                      <a href="https://www.1x2live.it/" style="color: #ad1e24;"
                        >Registrati per accedere.</a
                      >
                    </p>
                  </v-flex>
                </v-layout>
                <v-divider></v-divider>
              </v-card-actions>
            </v-card>
            <p style="text-align:center; margin-top: 2em; font-size:small;">
              2019 Condivision 2.0 -
              <a href="//www.aryma.it/" style="color: #ad1e24;">
                made in aryma
              </a>
            </p>
          </v-col>
        </v-row>
        <!-- <v-layout align-center justify-left wrap>
          <v-flex xs12 sm8 md4>
            
          </v-flex>
        </v-layout> -->
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

          if (response.data.esito != "OK") {
            this.alertMessage = response.data.esito;
          }

          if (response.data.redirect || response.data.includes("redirect")) {
            // window.location.href = response.data.redirect;
            window.location.href = location.origin;
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
