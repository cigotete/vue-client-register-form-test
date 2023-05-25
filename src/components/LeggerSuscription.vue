<template>
  <main class="container-main">
    <div class="container-main__col container-main__col--left">
      adfadfadsf
    </div>
    <div class="container-main__col container-main__col--right">
      <section class="page">
        <h1>Inscripción punto de venta</h1>
        <div v-if="errorRequest">
          Se ha presentado un error, por favor intente nuevamente mas tarde.
        </div>
        <ul  v-if="validationErrors">
          <li v-for="(error, field) in validationErrors" :key="field">
            {{ error }}
          </li>
        </ul>

        <form v-if="showForm" id="legger-form" class="legger-form" @submit="submitForm">
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
          <div>
            <h2>Términos y Condiciones</h2>
            <ul>
              <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque.</li>
              <li>At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium voluptatum deleniti atque corrupti quos dolores et quas.</li>
              <li>Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</li>
            </ul>

            <h2>Política de Tratamiento de Datos</h2>
            <ul>
              <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque.</li>
              <li>At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium voluptatum deleniti atque corrupti quos dolores et quas.</li>
              <li>Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</li>
            </ul>
          </div>

          <button type="submit" @click="cleanErrors()">Submit</button>
        </form>
        <div v-else>{{ successMessage }}</div>
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
      errorRequest: false,
      showForm: true,
      successMessage: '',
    };
  },
  methods: {
    validate_alphabet_characters(value) {
      console.log(value);
    },
    cleanErrors() {
      this.validationErrors = {};
      this.errorRequest = false;
    },
    submitForm(event) {
      event.preventDefault();
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
          // Check if the response data is defined
          if (response.data) {
            this.showForm = false;
            this.successMessage = 'Formulario enviado satisfactoriamente!';
          } else {
            // Handle the case when the response data is undefined
            console.log('Response data is undefined');
          }
        })
        .catch(error => {
          if (error.response && error.response.data && error.response.data.message) {
            const fieldNames = this.field_names;
            let error_str = error.response.data.message;
            // Replace the field names in the error message
            Object.keys(fieldNames).forEach(function (key) {
              var regex = new RegExp(key, 'g');
              error_str = error_str.replace(regex, fieldNames[key]);
            });
            // Remove the first line of the error message
            const remove_str = 'Unprocessable Entity: validation failed.\n';
            if (error_str.includes(remove_str)) {
              error_str = error_str.replace(remove_str, '');
            }
            // Remove the last line of the error message
            error_str = error_str.replace(/\n$/, '');
            this.validationErrors = error_str.split('\n');
          } else if (error.request) {
            // The request was made but no response was received
            console.error("error.request", error.request);
            // Display a custom error message indicating the network issue
            this.errorRequest = "Error de conexión, por favor intente mas tarde.";
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
