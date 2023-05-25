<template>
  <div v-if="validationErrors">
  <ul>
    <li v-for="(error, field) in validationErrors" :key="field">
      {{ error }}
    </li>
  </ul>
</div>
  <div id="legger-form">
    <label for="client-name">{{ this.field_names.field_legger_client_name }}</label>
    <input id="client-name" type="text" v-model="form.field_legger_client_name" :maxlength="255" required>
  
    <label for="client-nit">{{ this.field_names.field_legger_client_nit }}</label>
    <input id="client-nit" type="text" v-model="form.field_legger_client_nit" :maxlength="255" required>
  
    <label for="point-name">{{ this.field_names.field_legger_point_name }}</label>
    <input id="point-name" type="text" v-model="form.field_legger_point_name" :maxlength="255">
  
    <label for="team-name">{{ this.field_names.field_legger_team_name }}</label>
    <input id="team-name" type="text" v-model="form.field_legger_team_name" :maxlength="255">
  
    <label for="cities">{{ this.field_names.field_legger_cities }}</label>
    <select id="cities" v-model="form.field_legger_cities">
      <option v-for="city in cities" :key="city.key" :value="city.key">{{ city.value }}</option>
    </select>
  
    <label for="promoter-name">{{ this.field_names.field_legger_promoter }}</label>
    <input id="promoter-name" type="text" v-model="form.field_legger_promoter" :maxlength="255">
  
    <label for="rtc">{{ this.field_names.field_legger_rtc }}</label>
    <input id="rtc" type="text" v-model="form.field_legger_rtc" :maxlength="255">
  
    <label for="captain-user">{{ this.field_names.field_legger_captain_andor_user }}</label>
    <input id="captain-user" type="text" v-model="form.field_legger_captain_andor_user" :maxlength="255">
  
    <label for="accept-toc-pdt">
      <input id="accept-toc-pdt" type="checkbox" v-model="form.field_legger_accept_tnc_pdt" required>
      {{ this.field_names.field_legger_accept_tnc_pdt }}
    </label>

    <button @click="submitForm" type="submit">Submit</button>
  </div>
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
        field_legger_accept_tnc_pdt: 'Acceptar terminos y condiciones y Politica de tratamiento de datos',
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

<style>
input, select, button {
  display: block;
  margin: 5px 0px 10px 0px;
}

#legger-form {
  width: 50%;
  text-align: left;
}
</style>
