<template>
  <div>
    <b-modal id="bv-modal-example" hide-footer>
      <template v-slot:modal-title>
        Search film
      </template>
      <div class="d-block text-center">
        <b-form-input v-model="inputFilm" @keyup.enter="search" />
      </div>
      <b-button class="mt-3" block @click="search">
        Search
      </b-button>
    </b-modal>

    <b-navbar toggleable="lg" type="dark">
      <b-navbar-nav class="ml-auto">
        <b-button size="sm" class="my-2 my-sm-0" @click="$bvModal.show('bv-modal-example')">
          <svg
            id="Capa_1"
            enable-background="new 0 0 515.558 515.558"
            height="20"
            viewBox="0 0 515.558 515.558"
            width="20"
            fill="#4285f4"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path d="m378.344 332.78c25.37-34.645 40.545-77.2 40.545-123.333 0-115.484-93.961-209.445-209.445-209.445s-209.444 93.961-209.444 209.445 93.961 209.445 209.445 209.445c46.133 0 88.692-15.177 123.337-40.547l137.212 137.212 45.564-45.564c0-.001-137.214-137.213-137.214-137.213zm-168.899 21.667c-79.958 0-145-65.042-145-145s65.042-145 145-145 145 65.042 145 145-65.043 145-145 145z" /></svg>
        </b-button>
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
export default {
  data () {
    return {
      inputFilm: ''
    }
  },
  methods: {
    search () {
      this.$bvModal.hide('bv-modal-example')
      this.$router.push({ path: '/search', query: { query: this.inputFilm } })
      this.inputFilm = ''
    }
  }
}
</script>

<style>
  .navbar {
    background-color: #032541;
    justify-content: right;
  }

  .form-inline {
    flex-flow: nowrap;
  }

  .btn-secondary {
    color: #fff;
    background-color: #032541;
    border-color: #032541;
  }

</style>
