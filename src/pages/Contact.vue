<template>
  <Layout>
    <div class="container">
      <div class="contact-header">
        <h1 class="contact-title">Contact Us</h1>
        <p>If you have any questions, please contact us by telephone, email or fill the form below and we'll get back to you as soon as possible.</p>
        <p>We look forward to hearing from you.</p>
        <br>
        <p>
          Phone:
          <a href="tel:+265999950917">+265 886 585 999</a>
        </p>
        <p>
          Email:
          <a href="mailto:info@chrinas.com">info@chrinas.com</a>
        </p>
        <p>Area 47, Sector 1</p>
        <p>Lilongwe, Malawi</p>
      </div>

      <form
        class="contact-form"
        name="contact"
        v-on:submit.prevent="handleSubmit"
        method="POST"
        data-netlify="true"
        data-netlify-honeypot="bot-field"
      >
        <input type="hidden" name="form-name" value="contact">

        <div class="sender-info">
          <div>
            <label for="name" class="label">Your name</label>
            <input type="text" name="name">
          </div>
          <div>
            <label for="email" class="label">Your email</label>
            <input type="email" name="email">
          </div>
        </div>

        <div class="message">
          <label for="message" class="label">Message</label>
          <textarea name="message"></textarea>
        </div>

        <button class="button" type="submit" :disabled="disable">Submit form</button>

        <p>{{ status }}</p>
      </form>
    </div>
  </Layout>
</template>

<script>
export default {
  data() {
    return {
      formData: {},
      status: "",
      disable: false
    };
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
            "Thank You! Your message has been sent. We will get back to you as soon as we can";
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

