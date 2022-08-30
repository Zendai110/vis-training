<template>
  <div id="confirm-msg" class="message" v-if="showConfirmation">
    <div></div>
    Thank you for your time. Details have been successfully submitted.
    <button @click.prevent="close()" class="close-button">x</button>
  </div>
  <header style="text-align: center">
    <img
      style="width: 150px; margin-top: 20px"
      src="./assets/VIS-Networks-Logo.png"
    />
  </header>
  <main class="middle">
    <div class="item"></div>
    <div class="content">
      <h2>Contact Us</h2>

      <form>
        <label for="fname">First Name</label>
        <input
          type="text"
          id="fname"
          name="firstname"
          v-model="v$.fname.$model"
        />
        <div class="error-msg" v-if="v$.fname.$error">
          First Name is required
        </div>
        <br />

        <label for="lname">Last Name</label>
        <input
          type="text"
          id="lname"
          name="lastname"
          v-model="v$.lname.$model"
        />
        <div class="error-msg" v-if="v$.lname.$error">
          Last Name is required
        </div>
        <br />

        <label for="tel">Telephone</label>
        <input type="text" id="tel" name="telephone" v-model="v$.tel.$model" />
        <div class="error-msg" v-if="v$.tel.$error">Telephone is required</div>
        <br />

        <label for="country">Country</label>
        <select id="country" name="country" v-model="country">
          <option value="">Please Select ...</option>
          <option value="australia">Australia</option>
          <option value="canada">Canada</option>
          <option value="usa">USA</option>
        </select>

        <label for="subject">Subject</label>
        <textarea
          id="subject"
          name="subject"
          style="height: 150px"
          v-model="v$.subject.$model"
        ></textarea>
        <div class="error-msg" v-if="v$.subject.$error">
          Subject is required
        </div>
        <br />

        <input
          type="submit"
          value="Submit"
          id="submission"
          @click.prevent="updateConfirmation()"
        />
      </form>
    </div>
    <div class="item"></div>
  </main>
  <footer></footer>
</template>

<script setup>
import { ref, computed } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { minLength, required } from "@vuelidate/validators";

const showConfirmation = ref(false);
const fname = ref(null);
const lname = ref(null);
const tel = ref(null);
const country = ref("");
const subject = ref(null);
const rules = computed(() => ({
  fname: { required },
  lname: { required },
  tel: { required },
  subject: { required },
}));
const v$ = useVuelidate(rules, { fname, lname, tel, subject });
const updateConfirmation = () => {
  showConfirmation.value = true;
  fname.value = null;
  lname.value = null;
  tel.value = null;
  country.value = "";
  subject.value = null;
  v$.value.$reset();
};
const close = () => {
  showConfirmation.value = false;
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
.middle {
  display: flex;
  flex-direction: row;
}

.item {
  height: 100px;
  width: 600px; /* A fixed width as the default */
}

.content {
  flex-grow: 1; /* Set the middle element to grow and stretch */
}

.item + .item {
  margin-left: 2%;
}

h2 {
  font-size: 40px;
  color: rgba(237, 67, 37, 1);
}
label {
  color: rgb(94, 94, 94);
}
input[type="text"],
select,
textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid rgb(230, 230, 230);
  background: rgb(245, 245, 245);
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
}

input[type="text"]:focus,
select:focus,
textarea:focus {
  background: rgb(255, 255, 255);
}

input[type="submit"] {
  width: 100%;
  background-color: rgb(196, 64, 152);
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 20px;
}

input[type="submit"]:hover {
  background-color: rgb(158, 32, 116);
}

.message {
  position: fixed;
  top: 25px;
  left: 50%;
  transform: translateX(-50%);
  margin-block-end: 20px;
  background-color: rgba(237, 67, 37, 0.9);
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  color: #fff;
}

.close-button {
  border-radius: 50%;
  height: 35px;
  width: 35px;
  border: transparent;
  /* padding: 10px; */
  margin: 2px;
  text-align: center;
}

.close-button:hover {
  background: rgb(199, 199, 199);
  cursor: pointer;
}
.error-msg {
  color: #cd2122;
  font-size: 12px;
  margin-block-end: 0px;
}
</style>
