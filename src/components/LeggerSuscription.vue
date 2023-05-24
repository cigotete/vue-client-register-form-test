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
  </div>
</template>

<script>
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
    }
  }
};
</script>

<style>
input, select {
  display: block;
  margin-bottom: 10px;
}

#legger-form {
  width: 50%;
  text-align: left;
}
</style>
