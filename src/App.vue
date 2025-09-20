<script setup>
import { email, min, required } from "@vee-validate/rules";
import { defineRule, ErrorMessage, Field, Form } from "vee-validate";
import { reactive } from "vue";

const data = reactive({
  name: "",
  email: "",
  subject: "",
  message: "",
  extras: [],
  gender: "",
});


defineRule('required', required);
defineRule('email', email);
defineRule('min', min);


function submitForm() {
  alert(JSON.stringify(data, null, 2));
}


</script>

<template>
  <h1>Contact Person</h1>
  <Form @submit="submitForm">
    <div>
      <label for="name">Name</label>
      <Field name="name" type="text" :rules="required" id="name" v-model.lazy="data.name" />
      <ErrorMessage as="text" name="name" />
    </div>
    <div>
      <label for="email">Email</label>
      <Field name="email" type="email" rules="email|required" v-model.lazy="data.email" />
      <ErrorMessage as="text" name="email" />
    </div>
    <div>
      <label for="gender">Gender</label>
      <Field name="gender" as="select" rules="required" id="gender" v-model.lazy="data.gender">
        <option value="Male">Male</option>
        <option value="Female">Female</option>
      </Field>
      <ErrorMessage as="text" name="gender" />

    </div>
    <div>
      <label for="subject">Subject</label>
      <Field name="subject" type="text" :rules="required" id="subject" v-model.lazy="data.subject" />
      <ErrorMessage as="text" name="subject" />
    </div>

    <div>
      <label for="message">Message</label>
      <Field name="message" rules="required|min:20" as="textarea" id="message" rows="3" v-model.lazy="data.message" />
      <ErrorMessage as="text" name="message" />
    </div>

    <fieldset>
      <legend>Extras ?</legend>
      <div>
        <Field name="extras" type="checkbox" rules="required" value="Newslater" id="newslater" v-model="data.extras" />
        <label for="newslater">Newslater</label>
      </div>
      <div>
        <Field name="extras" type="checkbox" rules="required" value="Promotion" id="promotion" v-model="data.extras" />
        <label for="promotion">Promotion</label>
      </div>
      <ErrorMessage as="text" name="extras" />
    </fieldset>

    <button>Submit Form</button>
  </Form>
</template>
<style scoped>
h1 {
  color: olive;
}

form {
  background-color: beige;
  height: auto;
  padding: 35px;
  border-radius: 12px;
  display: flex;
  gap: 20px;
  flex-direction: column;
  text-align: start;

  button {
    margin-top: 15px;
    background-color: olive;
    color: oldlace;
    font-weight: bold;
  }
}

fieldset {
  border-radius: 12px;
  border: solid 1px olive;
  font-weight: bold;
  color: olive;
  legend {
    font-weight: bold;
    color: olive;
    /* margin-left: 12px; */
  }

  div {
    display: flex;
    flex-direction: row;
    margin: 5px;
    gap: 10px;

    input:checked {
      accent-color: olive;
    }
  }
}

div {
  display: flex;
  flex-direction: column;
  font-weight: bold;
  color: olive;

  input,
  select,
  textarea {
    border: 1px solid olive;
    border-radius: 12px;
    padding: 10px;
  }
}
</style>
