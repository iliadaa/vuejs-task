<template>
  <v-card class="mx-auto px-6 pt-8 pb-6 card-form" max-width="450px">
    <v-form ref="form">
      <div class="text-center">
        <h3 class="form-header">Please fill out this form</h3>
      </div>
      <v-text-field v-model="formData.name" label="Name" class="custom-text-field" variant="solo"></v-text-field>
      <v-text-field v-model="formData.surname" label="Surname" class="custom-text-field" variant="solo"></v-text-field>
      <v-text-field v-model="formData.email" label="Email" type="text" :rules="emailRules" class="custom-text-field"
        variant="solo"></v-text-field>
      <v-text-field v-model="formData.age" @keypress="filterNumbers(event)" label="Age" type="text" :rules="ageRules"
        class="custom-text-field" variant="solo"></v-text-field>
      <v-select v-model="formData.favoriteColor" :items="colorOptions" label="Favorite color" class="custom-text-field"
        variant="solo" hide-details>
      </v-select>

      <v-container class="pa-2">
        <h5 class="contact-preference-label">Choose contact preference</h5>
        <v-row>
          <v-col cols="4" class="pa-0">
            <v-checkbox v-model="formData.contactPreference" :rules="[contactPreferenceRule]" label="by email"
              value="Email" color="blue-lighten-3" class="contact-preference-details"></v-checkbox>
          </v-col>
          <v-col cols="4" class="pa-0">
            <v-checkbox v-model="formData.contactPreference" :rules="[contactPreferenceRule]" label="by phone call"
              value="Phone Call" color="blue-lighten-3" class="contact-preference" hide-details></v-checkbox>
          </v-col>
          <v-col cols="4" class="pa-0">
            <v-checkbox v-model="formData.contactPreference" :rules="[contactPreferenceRule]" label="via SMS"
              value="via SMS" color="blue-lighten-3" class="contact-preference" hide-details></v-checkbox>
          </v-col>
        </v-row>
      </v-container>

      <v-container class="d-flex justify-center pt-0">
        <v-btn class="me-4 submit-button mt-3" @click="submitForm">Submit</v-btn>
      </v-container>
    </v-form>
  </v-card>
</template>

<script>
export default {
  name: "FormLayout",
  data() {
    return {
      formData: {
        name: "",
        surname: "",
        email: "",
        age: "",
        favoriteColor: "",
        contactPreference: [],
      },
      colorOptions: ["Red", "Green", "Blue", "White", "Black"],
      emailRules: [(v) => /.+@.+\..+/.test(v) || "Email must be a valid email address"],
      ageRules: [(v) => v < 120 || "Age must be less than 120"],
    };
  },
  computed: {
    contactPreferenceRule() {
      return () =>
        this.formData.contactPreference?.length > 0 ||
        "Please select at least one contact preference.";
    },

  },
  methods: {


    //make input only numbers
    filterNumbers(evt) {
      evt = evt ? evt : window.event;
      let expect = evt.target.value.toString() + evt.key.toString();
      if (!/^[-+]?[0-9]*\.?[0-9]*$/.test(expect)) {
        evt.preventDefault();
      } else {
        return true;
      }
    },

    submitForm() {
      if (this.$refs.form.validate()) {
        if (
          this.formData.name.trim() === "" ||
          this.formData.surname.trim() === ""
        ) {
          return;
        }
        this.$emit("form-submitted", this.formData);

        this.$nextTick(() => {
          this.formData = {
            name: "",
            surname: "",
            email: "",
            age: "",
            favoriteColor: "",
            contactPreference: [""],
          };
        });

        this.$refs.form.resetValidation()

      }
    },
  },
};
</script>

<style>
.card-form {
  margin: 0 auto;
  border-radius: 8px;
  box-shadow: 0px 1px 4px 0px rgba(0, 0, 0, 0.25);
}

.form-header {
  color: #43546f;
  font-weight: 700;
  margin-bottom: 16px;
}

.contact-preference-label {
  color: #435673;
  font-size: 14px;
  font-weight: 500;
  margin-left: 5px;
  padding-bottom: 5px;
  padding-top: 5px;
  margin-bottom: 5px;
}

.v-field__input {
  height: 50px;
  min-height: 0;
  padding-top: 22px;
}

.v-field__field {
  font-family: "Roboto", sans-serif;
  background-color: #f3f8ff;
  border-radius: 8px;
}

.v-field__outline {
  border: 1px solid #cfdeff;
  border-radius: 10px;
}

.v-label {
  color: #43546f;
  font-family: "Roboto", sans-serif;
  font-size: 12px;
  font-style: normal;
  font-weight: 500;
}

.v-field--variant-solo,
.v-field--variant-solo-filled {
  border-radius: 8px;
  box-shadow: none;
}

.v-input__details {
  padding: 2px;
  min-height: 15px;
  width: max-content;
}

.contact-preference-details>.v-input__details {
  margin-top: -10px;
  margin-left: 50%;
}

.v-checkbox .v-selection-control {
  min-height: 40px;
}

.submit-button {
  border-radius: 10px;
  background-color: #0e55cb;
  color: #fff;
  font-size: 15px;
  font-style: normal;
  font-weight: 500;
  width: 50%;
  text-transform: capitalize;
}
</style>
