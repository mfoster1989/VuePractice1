<template>
  <div id="app">
		<TheHeader/>
        <main>
        <TheJobList v-bind:jobListData="listingData"/>
        <TheJobForm :sendListing="postListing"/>
        </main>

		<TheFooter/>

	</div>
</template>

<script>
import TheHeader from "./components/TheHeader"
import TheFooter from "./components/TheFooter"
import TheJobList from "./components/TheJobList"
import TheJobForm from "./components/TheJobForm"

export default {
  name: 'App',
  components: {
		TheHeader,
		TheFooter,
		TheJobList,
        TheJobForm
	},
	data() {
		return {
			apiURL: "../static/listings.json",
			listingData: []
		}
	},
	mounted() {
	  this.getListings();
	},
	methods: {
	  getListings() {
			fetch(this.apiURL)
			.then(response => response.json())
			.then(response => {
				this.listingData = response;
			})
	  },
      postListing(listing) {
          this.listingData.unshift(listing)
      },
  }
}

</script>

<style>

main {
    grid-row: 2/3;
    display: grid;
    grid-template-columns: 5% 42.5% 5% 42.5% 5%;
}

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin-top: 60px;
	margin: 0 30px 0 30px;
	padding: 0;
	color: #1B997A;
	display: grid;
	grid-template-rows: 15% 75% 10%;
}

</style>
