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
        src="https://secure.1x2live.it/fl_config/secure.1x2live.it/img/logo.jpg"
        max-height="100%"
        contain
      ></v-img>
    </v-app-bar>

    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center wrap>
          <template v-if="x === null || y === null">
            <v-alert type="error">
              Errore 404: Non dovresti essere qui
            </v-alert>
            <a :href="rootPath"></a>
          </template>
          <v-flex v-else xs12 sm8 md4>
            <v-form @submit.prevent="handleSubmit">
              <v-card class="elevation-2">
                <v-toolbar dark color="black" flat>
                  <v-toolbar-title>Recupera Password</v-toolbar-title>
                </v-toolbar>
                <v-card-text>
                  <v-alert v-if="alertMessage" :type="alertType">
                    {{ alertMessage }}
                  </v-alert>

                  <v-text-field
                    v-model="password"
                    placeholder="Password"
                    color="#ad1e24"
                    name="password"
                    prepend-icon="mdi-account"
                    type="password"
                  ></v-text-field>

                  <v-text-field
                    v-model="confirm"
                    placeholder="Conferma Password"
                    color="#ad1e24"
                    name="password-confirm"
                    prepend-icon="mdi-account"
                    type="password"
                  ></v-text-field>
                </v-card-text>
                <v-card-actions>
                  <v-layout justify-center wrap class="mb-4">
                    <v-flex style="text-align:center" xs12>
                      <v-btn
                        style="padding: 0 2em; margin: 0 auto;"
                        dark
                        color="#ad1e24"
                        :loading="loading"
                        type="submit"
                        >Resetta</v-btn
                      >
                    </v-flex>
                  </v-layout>
                </v-card-actions>
              </v-card>
            </v-form>

            <p style="text-align:center; margin-top: 2em;">
              2019 1x2live.it
            </p>
          </v-flex>
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
    password: "",
    confirm: "",
    ip: "",
    loading: false,
    formData: new FormData(),
    x: null,
    y: null,
    alertType: "error",
    rootPath: null
  }),
  methods: {
    handleSubmit() {
      console.log("sent");
      if (this.password !== this.confirm) {
        this.alertType = "error";
        this.alertMessage = "Le password non sono le stesse";
        return;
      }
      this.formData.append("resetPassword", true);
      this.formData.append("x", this.x);
      this.formData.append("y", this.y);
      this.formData.append("password", this.password);

      this.alertMessage = "";
      this.loading = true;

      const host =
        location.hostname === "localhost"
          ? "secure.1x2live.it"
          : location.hostname;

      axios
        .post(`https://${host}/fl_api/resetPassword.php`, this.formData, {
          headers: {
            "Content-Type": "multipart/form-data"
          }
        })
        .then(response => {
          this.loading = false;
          console.log(response);

          if (response.data.status) {
            this.alertType = "success";
            this.alertMessage = response.data.message;
          }

          // if (response.data.redirect || response.data.includes("redirect")) {
          //   // window.location.href = response.data.redirect;
          //   window.location.href = location.origin;
          // }
        })
        .catch(error => {
          this.loading = false;
          console.log(error);
        });
    }
  },
  created() {
    let uri = window.location.search.substring(1);
    let params = new URLSearchParams(uri);
    this.x = params.get("x");
    this.y = params.get("y");
    this.rootPath = `https://${location.hostname}`;

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
