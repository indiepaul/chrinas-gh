<template>
  <Layout>
    <div class="container">
      <div class="contact-header">
        <h1 class="contact-title">Book Now</h1>
        <p>Leave your details and our agent will get in touch as soon as possible.</p>
      </div>

      <form class="contact-form" name="contact">
        <div class="sender-info">
          <div>
            <label for="name" class="label">Your name</label>
            <input type="text" name="name">
          </div>
        </div>
        <div class="sender-info">
          <div>
            <label for="email" class="label">Your email</label>
            <input type="email" name="email">
          </div>
          <div>
            <label for="email" class="label">Phone Number</label>
            <input type="email" name="email">
          </div>
        </div>

        <div class="sender-info">
          <div>
            <label for="checkin" class="label">Check In</label>
            <input type="date" name="checkin">
          </div>
          <div>
            <label for="duration" class="label">Duration</label>
            <select name="duration">
              <option
                v-for="price in prices"
                :key="price.duration"
              >{{price.duration}} {{price.duration == 1 ? 'Day' : 'Days'}}: K{{price.kwacha}}/£{{price.pounds}}</option>
            </select>
          </div>
        </div>

        <div class="message">
          <label for="message" class="label">Message</label>
          <textarea name="message"></textarea>
        </div>

        <button class="button">Submit form</button>
      </form>
    </div>
  </Layout>
</template>

<script>
import prices from "../../data/prices.json";

export default {
  data() {
    return {
      prices: prices.price_list.reverse()
    };
  }
};
</script>

<style scoped>
.contact-header {
  padding: 2rem 0 4rem 0;
}
.contact-title {
  font-size: 4rem;
  margin: 0 0 4rem 0;
  padding: 0;
}
.sender-info {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}
.sender-info > div {
  flex: 1;
  margin-right: 4rem;
}
.sender-info > div:last-of-type {
  margin: 0;
}
input:focus,
textarea:focus {
  border-color: var(--theme-color);
}
input,
textarea {
  background: transparent;
  border: 1px solid var(--color-base-1);
  outline: none;
  border-radius: 0.3rem;
  padding: 0.8rem 1rem;
  color: inherit;
  font-size: 1rem;
  width: 100%;
}
textarea {
  resize: none;
  height: 140px;
}
.button {
  color: var(--color-contrast);
  background: var(--theme-color);
  outline: none;
  border: 0;
  font-size: 0.8rem;
  padding: 0.8rem 1.6rem;
  border-radius: 0.3rem;
  margin-top: 2rem;
  cursor: pointer;
  transition: opacity 0.25s ease;
  font-size: 500;
  letter-spacing: 0.035em;
}
.button:hover {
  opacity: 0.6;
}
.button:focus {
  border: 1px solid var(--color-base-1);
}
</style>

