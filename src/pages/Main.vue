<template>
  <div class="w-full flex">
    <div class="m-auto">
      <h1 class="text-3xl text-center">Url Shortening Service</h1>
      <form>
        <div class="text-center my-8">
          <input
            v-model="url"
            type="url"
            name="url"
            class="border rounded py-2 my-2"
            placeholder="Enter url to shorten"
            @input="change()"
            @change="change()"
          />
          <button
            v-on:click.prevent="onSubmit"
            type="submit"
            class="border rounded bg-gradient-to-r from-red-700 to-pink-700 text-white items-center py-2 ml-2 px-2"
          >
            Submit
          </button>
        </div>
        <h2 v-if="!isValid" v-bind:style="{ display: showError, marginTop: '20px' }">
          Invalid URL Entered, URL should start with http/https
        </h2>
        <div v-if="processing" class="text-center">
          <div class="spinner-border" role="status">
            <span class="sr-only">Loading...</span>
          </div>
        </div>
        <h3 v-if="shorted">
          <div>
            <button
              type="button"
              class="border rounded bg-gradient-to-r from-gray-800 to-green-700 text-white items-center py-2 px-2 mr-2 text-lg"
              style="pointer-events:none"
            >
              Your Shorten Url :
            </button>
            <a
              :href="`https://s-urls.herokuapp.com/${shortenurl}`"
              style="text-decoration:underline"
              class="text-xl"
              target="_blank"
              ><pre style="display:inline;">s-urls.herokuapp.com/</pre>
              {{ shortenurl }}</a
            >
          </div>
        </h3>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "",
      shorted: false,
      shortenurl: "",
      isValid: false,
      processing: false,
      regex:
        // "/(http(s)?://.)(www.)?[-a-zA-Z0-9@:%._+~#=]{2,256}.[a-z]{2,6}b([-a-zA-Z0-9@:%_+.~#?&//=]*)/",
        "https?://(www.)?",
      showError: "none",
    };
  },
  methods: {
    onSubmit() {
      if (!this.isValid) {
        console.log("false");
        this.shorted = false;
        this.showError = "block";
        return;
      }
      this.showError = "none";
      this.shorted = false;
      this.processing = true;
      this.axios
        .post("https://s-urls.herokuapp.com/?fullurl=" + this.url)
        .then((res) => {
          console.log(res);
          this.shorted = true;
          this.shortenurl = res.data;
          this.processing = false;
        })
        .catch(() => {
          this.processing = false;
        });
    },
    change() {
      // console.log("change");
      let re = new RegExp(this.regex);
      if (re.test(this.url)) {
        this.isValid = true;
      } else {
        this.isValid = false;
      }
      // this.isValid = this.url.match(this.regex);
      // this.isValidURL(this.url);
      // console.log(this.isValid);
    },
    // isValidURL(url) {
    //   this.isValid = url.match(this.regex);
    // },
  },
};
</script>

<style>
input {
  caret-color: green;
}
</style>
