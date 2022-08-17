<template>
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
      <div id="confirm-msg" class="message" v-if="showConfirmation">
        Details have been successfully submitted
      </div>

      <form>
        <label for="fname">First Name</label>
        <input type="text" id="fname" name="firstname" v-model="fname" />

        <label for="lname">Last Name</label>
        <input type="text" id="lname" name="lastname" v-model="lname" />

        <label for="tel">Telephone</label>
        <input type="text" id="tel" name="telephone" v-model="tel" />

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
          v-model="subject"
        ></textarea>

        <input
          type="submit"
          value="Submit"
          @click.prevent="updateConfirmation()"
        />
      </form>
    </div>
    <div class="item"></div>
  </main>
  <footer></footer>
</template>

<script setup>
import { ref } from "vue";
const showConfirmation = ref(false);
const fname = ref("");
const lname = ref("");
const tel = ref("");
const country = ref("");
const subject = ref("");
function updateConfirmation() {
  showConfirmation.value = true;
  fname.value = "";
  lname.value = "";
  tel.value = "";
  country.value = "";
  subject.value = "";
}
</script>

<style scoped>
* {
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
.middle {
  display: flex;
}

.item {
  height: 100px;
  width: 800px; /* A fixed width as the default */
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
  margin-block-end: 20px;
  background-color: rgba(237, 67, 37, 0.267);
  border-radius: 5px;
  padding: 10px;
  text-align: center;
}
</style>
