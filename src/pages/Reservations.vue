<template>
  <Layout>
    <div class="container">
      <img :src="image" alt="Price List" />
    </div>
    <div class="container">
      <div class="contact-header">
        <h1 class="contact-title">Reservations</h1>
        <p>
          Leave your details and our agent will get in touch as soon as
          possible.
        </p>
      </div>

      <form
        class="contact-form"
        name="bookings"
        v-on:submit.prevent="handleSubmit"
        method="POST"
        data-netlify="true"
        data-netlify-honeypot="bot-field"
      >
        <input type="hidden" name="form-name" value="bookings" />
        <div class="sender-info">
          <div>
            <label for="name" class="label">Your name</label>
            <input type="text" name="name" v-model="formData.name" required />
          </div>
        </div>
        <div class="sender-info">
          <div>
            <label for="email" class="label">Your email</label>
            <input
              type="email"
              name="email"
              v-model="formData.email"
              required
            />
          </div>
          <div>
            <label for="phone" class="label">Phone Number</label>
            <input
              type="phone"
              name="phone"
              v-model="formData.phone"
              required
            />
          </div>
        </div>

        <div class="sender-info">
          <div>
            <label for="Room" class="label">Room</label>
            <div>
              <input
                type="radio"
                name="room"
                id="main room"
                value="main"
                v-model="formData.room"
                required
              />
              <label for="main room">Main Room</label>
            </div>
            <div>
              <input
                type="radio"
                name="room"
                id="room two"
                value="two"
                v-model="formData.room"
                required
              />
              <label for="room two">2nd Room</label>
            </div>
          </div>
          <div>
            <label for="occupants" class="label">Occupants</label>
            <div>
              <input
                type="radio"
                name="occupants"
                id="one"
                value="one"
                v-model="formData.occupants"
                required
              />
              <label for="one">One</label>
            </div>
            <div>
              <input
                type="radio"
                name="occupants"
                id="two"
                value="two"
                v-model="formData.occupants"
                required
              />
              <label for="two">Two</label>
            </div>
          </div>
        </div>

        <div class="sender-info">
          <div>
            <label for="checkin" class="label">Check In</label>
            <input
              type="date"
              name="checkin"
              v-model="formData.checkin"
              required
            />
          </div>
          <div>
            <label for="duration" class="label">Duration</label>
            <select name="duration" v-model="formData.duration" required>
              <option v-for="price in Object.keys(prices)" :key="price">{{
                price
              }}</option>
            </select>
          </div>
        </div>
        <p>
          Price:
          <b>{{ price }}</b>
        </p>
        <div class="message">
          <label for="message" class="label">Message</label>
          <textarea name="message" v-model="formData.message"></textarea>
        </div>
        <button class="button" type="submit">Submit form</button>
        <p>{{ status }}</p>
      </form>
    </div>
  </Layout>
</template>


<script>
  import prices from "../../data/prices.json";

  export default {
    data() {
      return {
        prices: prices.price_list,
        image: prices.image,
        formData: {},
        status: "",
        disable: false
      };
    },
    computed: {
      price() {
        var formData = this.formData;
        if (
          formData &&
          formData["room"] &&
          formData["occupants"] &&
          formData["duration"]
        )
          return new Intl.NumberFormat("en-US", {
            style: "currency",
            currency: "MWK",
            minimumFractionDigits: 2
          }).format(
            this.prices[formData["duration"]][
              formData["room"] + "-" + formData["occupants"]
            ]
          );
        return "";
      }
    },
    methods: {
      encode(data) {
        return Object.keys(data)
          .map(
            key => encodeURIComponent(key) + "=" + encodeURIComponent(data[key])
          )
          .join("&");
      },
      handleSubmit(e) {
        this.status = "Sending...";
        this.disable = true;
        fetch("/", {
          method: "POST",
          headers: { "Content-Type": "application/x-www-form-urlencoded" },
          body: this.encode({
            "form-name": e.target.getAttribute("name"),
            ...this.formData
          })
        })
          .then(() => {
            this.status =
              "Thank You! Your reservation has been sent. We will get back to you as soon as we can";
            this.disable = false;
          })
          .catch(error => {
            this.status = "Error sending message";
            this.disable = false;
          });
      }
    }
  };
</script>

<style scoped>
  input[type="radio"] {
    width: auto;
    margin-right: 1em;
  }
  .required {
    color: #aaa;
    font-size: 0.8rem;
  }
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

