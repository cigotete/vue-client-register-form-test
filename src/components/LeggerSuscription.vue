<template>
  <div id="legger-form">
    <label for="client-name">Client Name</label>
    <input id="client-name" type="text" v-model="form.clientName" :maxlength="255" required>
  
    <label for="client-nit">Client NIT</label>
    <input id="client-nit" type="text" v-model="form.clientNit" :maxlength="255" required>
  
    <label for="point-name">Point Name</label>
    <input id="point-name" type="text" v-model="form.pointName" :maxlength="255">
  
    <label for="team-name">Team Name</label>
    <input id="team-name" type="text" v-model="form.teamName" :maxlength="255">
  
    <label for="cities">Cities</label>
    <select id="cities" v-model="form.selectedCity">
      <option v-for="city in cities" :key="city.key" :value="city.key">{{ city.value }}</option>
    </select>
  
    <label for="promoter-name">Promoter Name</label>
    <input id="promoter-name" type="text" v-model="form.promoterName" :maxlength="255">
  
    <label for="rtc">RTC</label>
    <input id="rtc" type="text" v-model="form.rtc" :maxlength="255">
  
    <label for="captain-user">Captain and/or User</label>
    <input id="captain-user" type="text" v-model="form.captainUser" :maxlength="255">
  
    <label for="accept-toc-pdt">
      <input id="accept-toc-pdt" type="checkbox" v-model="form.acceptTocPdt" required>
      Accept Terms and Conditions
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
        clientName: '',
        clientNit: '',
        pointName: '',
        teamName: '',
        selectedCity: '',
        promoterName: '',
        rtc: '',
        captainUser: '',
        acceptTocPdt: false
      },
      cities: [
        { key: 'bogota', value: 'Bogotá' },
        { key: 'medellin', value: 'Medellín' },
        { key: 'cali', value: 'Cali' }
      ]
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
            value: this.form.clientName + ' - ' + this.form.clientNit,
          },
        ],
        field_legger_client_name: [
          {
            value: this.form.clientName,
          },
        ],
        field_legger_client_nit: [
          {
            value: this.form.clientNit,
          },
        ],
        field_legger_point_name: [
          {
            value: this.form.pointName,
          },
        ],
        field_legger_team_name: [
          {
            value: this.form.teamName,
          },
        ],
        field_legger_cities: [
          {
            value: this.form.selectedCity,
          },
        ],
        field_legger_promoter: [
          {
            value: this.form.promoterName,
          },
        ],
        field_legger_rtc: [
          {
            value: this.form.rtc,
          },
        ],
        field_legger_captain_andor_user: [
          {
            value: this.form.captainUser,
          },
        ],
        field_legger_accept_tnc_pdt: [
          {
            value: this.form.acceptTocPdt,
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
          console.error(error);
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
