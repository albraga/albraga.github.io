<template>
  <header></header>
  <main>
    <section class="mb-2 text-center container">
      <div class="row my-lg-5">
        <div class="col-md-8 mx-auto">
          <h1 class="font-weight-light">Alexandre Braga</h1>
          <p class="lead text-muted">
            Analista de Sistemas
          </p>
          <a href="mailto:albraga@email.com"
            ><img src="../assets/mail.svg" alt="mail" title="albraga@email.com"
          /></a>
          <span>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          <a href="https://github.com/albraga" target="blank"
            ><img src="../assets/github.svg" alt="github" title="github.com/albraga"
          /></a>
          <span>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          <a href="https://codeberg.org/albraga" target="blank"
            ><img src="../assets/codeberg.png" alt="github" title="codeberg.org/albraga"
          /></a>
          <span>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          <a href="https://www.linkedin.com/in/alexandre-braga-89ba29127/" target="blank"
            ><img src="../assets/linkedin.svg" alt="linkedin" title="linkedin"
          /></a>
          <span>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          <a href="https://www.facebook.com/alexandre.braga.9809" target="blank"
            ><img src="../assets/facebook.svg" alt="facebook" title="facebook"
          /></a>
        </div>
      </div>
    </section>

    <div class="container">
      <div class="row mb-3 justify-content-md-center">
        <div class="col col-md-2">
          <Portfolio />
        </div>
      </div>
      <div class="row mb-3">
        <div class="col-md-6">
          <SPA />
        </div>
        <div class="col-md-6">
          <HMA />
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <NMA />
        </div>
        <div class="col-md-6">
          <SSA />
        </div>
      </div>
    </div>
  </main>

  <footer></footer>
</template>

<script>
import Portfolio from './Portfolio.vue'
import SPA from './SPA.vue'
import HMA from './HMA.vue'
import NMA from './NMA.vue'
import SSA from './SSA.vue'

export default {
  components: {
    Portfolio,
    SPA,
    HMA,
    NMA,
    SSA
  }
}
</script>