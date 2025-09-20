<script setup>
import * as yup from "yup";
import { ErrorMessage, Field, Form } from "vee-validate";
import { reactive } from "vue";

const data = reactive({
  name: "",
  email: "",
  gender: "",
  subject: "",
  message: "",
  extras: [],
});

const schema = yup.object({
  name: yup.string().required(),
  email: yup
    .string()
    .required("Email gaboleh kosong")
    .email("Email mu ga valid nih"),
  gender: yup.string().required("Wajib punya kelamin!"),
  subject: yup.string().required("Subject gaboleh kosong"),
  message: yup.string().required("Message gaboleh kosong"),
  extras: yup.array().optional(),
});

function submitForm() {
  alert(JSON.stringify(data, null, 2));
}
</script>

<template>
  <h1>Contact Person</h1>
  <Form @submit="submitForm" :validation-schema="schema">
    <div>
      <label for="name">Name</label>
      <Field name="name" type="text" id="name" v-model.lazy="data.name" />
      <ErrorMessage class="error" name="name" />
    </div>
    <div>
      <label for="email">Email</label>
      <Field name="email" type="email" v-model.lazy="data.email" />
      <ErrorMessage class="error" as="text" name="email" />
    </div>
    <div>
      <label for="gender">Gender</label>
      <Field name="gender" as="select" id="gender" v-model.lazy="data.gender">
        <option value="Male">Male</option>
        <option value="Female">Female</option>
      </Field>
      <ErrorMessage class="error" as="text" name="gender" />
    </div>
    <div>
      <label for="subject">Subject</label>
      <Field
        name="subject"
        type="text"
        id="subject"
        v-model.lazy="data.subject"
      />
      <ErrorMessage class="error" as="text" name="subject" />
    </div>

    <div>
      <label for="message">Message</label>
      <Field
        name="message"
        as="textarea"
        id="message"
        rows="3"
        v-model.lazy="data.message"
      />
      <ErrorMessage class="error" as="text" name="message" />
    </div>

    <fieldset>
      <legend>Extras ?</legend>
      <div>
        <Field
          name="extras"
          type="checkbox"
          value="Newslater"
          id="newslater"
          v-model="data.extras"
        />
        <label for="newslater">Newslater</label>
      </div>
      <div>
        <Field
          name="extras"
          type="checkbox"
          value="Promotion"
          id="promotion"
          v-model="data.extras"
        />
        <label for="promotion">Promotion</label>
      </div>
      <ErrorMessage class="error" as="text" name="extras" />
    </fieldset>

    <button>Submit Form</button>
  </Form>
</template>
<style scoped>
h1 {
  color: olive;
}

.error {
  color: red;
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
