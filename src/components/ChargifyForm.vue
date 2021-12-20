<template>
  <div>
    <select v-on:change="changeItem">
      <option value="card">Credit Card</option>
      <option value="bank">Bank Account</option>
    </select>
    <br />
    <br />
    <form>
      <div id="chargify-form"></div>
      <label>
        Hidden Token: <input id="host-token" disabled v-model="token"/>
      </label>
      <p>
        <button v-on:click.prevent="handleClick">Submit Host Form</button>
      </p>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ChargifyForm',
  data: function() {
    return {
      chargify: new window.Chargify(),
      paymentType: 'card',
      token: '',
    }
  },
  mounted: function () {
    this.loadChargifyJs();
  },
  methods: {
    changeItem: function changeItem(event) {
      this.paymentType = event.target.value;

      this.loadChargifyJs();
    },
    handleClick: function () {
      this.chargify.token(
        document.querySelector('#chargify-form'),

        (token) => {
          console.log('{host} token SUCCESS - token: ', token);
          this.token = token;
        },

        (error) => {
          console.log('{host} token ERROR - err: ', error);
        }
      );
    },
    loadChargifyJs: function() {
      this.chargify.load({
        // selector where the iframe will be included in the host's HTML (i.e. '#chargify-form')
        // optional if you have a `selector` on each and every field
        selector: '#chargify-form',

        // (i.e. '1a2cdsdn3lkn54lnlkn')
        publicKey: 'MY_PUBLIC_KEY',

        // form type (possible values: 'card' or 'bank')
        type: this.paymentType || 'card',

        // points to your Chargify site
        serverHost: 'https://acme.chargify.test'
      });
    },
  }
}
</script>
