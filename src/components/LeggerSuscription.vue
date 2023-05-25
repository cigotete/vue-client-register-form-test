<template>
  <main class="container-main">
    <div class="container-main__col container-main__col--left">
      adfadfadsf
    </div>
    <div class="container-main__col container-main__col--right">
      <section class="page">
        <h1>Inscripción punto de venta</h1>

        <ul  v-if="validationErrors">
          <li v-for="(error, field) in validationErrors" :key="field">
            {{ error }}
          </li>
        </ul>

        <form id="legger-form" class="legger-form">
          <input id="client-name" type="text" :placeholder="field_names.field_legger_client_name" v-model="form.field_legger_client_name" :maxlength="255" required>    
          <input id="client-nit" type="text" :placeholder="this.field_names.field_legger_client_nit" v-model="form.field_legger_client_nit" :maxlength="255" required>
          <input id="point-name" type="text" :placeholder="this.field_names.field_legger_point_name" v-model="form.field_legger_point_name" :maxlength="255">
          <input id="team-name" type="text" :placeholder="this.field_names.field_legger_team_name" v-model="form.field_legger_team_name" :maxlength="255">
          <select id="cities" v-model="form.field_legger_cities">
            <option value="" disabled>{{this.field_names.field_legger_cities}}</option>
            <option v-for="city in cities" :key="city.key" :value="city.key">{{ city.value }}</option>
          </select>
          <input id="promoter-name" type="text" :placeholder="this.field_names.field_legger_promoter" v-model="form.field_legger_promoter" :maxlength="255">    
          <input id="rtc" type="text" :placeholder="this.field_names.field_legger_rtc" v-model="form.field_legger_rtc" :maxlength="255">    
          <input id="captain-user" type="text" :placeholder="this.field_names.field_legger_captain_andor_user" v-model="form.field_legger_captain_andor_user" :maxlength="255">    
          <label for="accept-toc-pdt">
            <input id="accept-toc-pdt" type="checkbox" v-model="form.field_legger_accept_tnc_pdt" required>
            {{ this.field_names.field_legger_accept_tnc_pdt }}
          </label>

          <button @click="submitForm" type="submit">Submit</button>
        </form>
      </section>
    </div>
  </main>
</template>

<script>
import axios from 'axios';
export default   {
  name: 'LeggerSuscription',
  data() {
    return {
      form: {
        field_legger_client_name: '',
        field_legger_client_nit: '',
        field_legger_point_name: '',
        field_legger_team_name: '',
        field_legger_cities: '',
        field_legger_promoter: '',
        field_legger_rtc: '',
        field_legger_captain_andor_user: '',
        field_legger_accept_tnc_pdt: false,
      },
      cities: [
        { key: 'bogota', value: 'Bogotá' },
        { key: 'medellin', value: 'Medellín' },
        { key: 'cali', value: 'Cali' }
      ],
      field_names: {
        field_legger_client_name: 'Nombre del cliente',
        field_legger_client_nit: 'NIT',
        field_legger_point_name: 'Nombre del punto',
        field_legger_team_name: 'Nombre del equipo',
        field_legger_cities: 'Ciudad',
        field_legger_promoter: 'Promotor',
        field_legger_rtc: 'RTC',
        field_legger_captain_andor_user: 'Capitan y/o usuario',
        field_legger_accept_tnc_pdt: 'Terminos y condiciones y Politica de Tratamiento de Datos',
      },
      validationErrors: {},
    };
  },
  methods: {
    validate_alphabet_characters(value) {
      console.log(value);
    },
    submitForm() {
      const data = {
        title: [
          {
            value: this.form.field_legger_client_name + ' - ' + this.form.field_legger_client_nit,
          },
        ],
        field_legger_client_name: [
          {
            value: this.form.field_legger_client_name,
          },
        ],
        field_legger_client_nit: [
          {
            value: this.form.field_legger_client_nit,
          },
        ],
        field_legger_point_name: [
          {
            value: this.form.field_legger_point_name,
          },
        ],
        field_legger_team_name: [
          {
            value: this.form.field_legger_team_name,
          },
        ],
        field_legger_cities: [
          {
            value: this.form.field_legger_cities,
          },
        ],
        field_legger_promoter: [
          {
            value: this.form.field_legger_promoter,
          },
        ],
        field_legger_rtc: [
          {
            value: this.form.field_legger_rtc,
          },
        ],
        field_legger_captain_andor_user: [
          {
            value: this.form.field_legger_captain_andor_user,
          },
        ],
        field_legger_accept_tnc_pdt: [
          {
            value: this.form.field_legger_accept_tnc_pdt,
          },
        ],
        type: [
          {
            target_id: 'legger_suscription',
          },
        ],
      };

      // Make an HTTP POST request to your endpoint
      axios
        .post('http://drupal-legger-test.test/node?_format=json', data)
        .then(response => {
          // Handle the response if needed
          console.log(response.data);
        })
        .catch(error => {
          // Handle the error if needed
          console.error(error.response.data.message);
          if (error.response && error.response.data && error.response.data.message) {
            this.validationErrors = error.response.data.message.split("\n");
            console.log(this.validationErrors);
          } else {
            console.error(error);
          }
        });
    },
  }
};
</script>

<style lang="scss">
@import "@/styles.scss";

</style>
