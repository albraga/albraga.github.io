<template>
  <div class="card">
    <h5 class="card-header">SPA</h5>
    <div class="card-body">
      <h5 class="card-title">Single-Page Application</h5>
      <p class="card-text">
        Projetos criados com
        <a href="https://v3.vuejs.org/" target="blank">Vue.js</a>,
        <a href="https://v5.getbootstrap.com/" target="blank">bootstrap</a>,
        além de diversos outros recursos.
      </p>
      <!-- Button trigger modal -->
      <button
        type="button"
        class="btn btn-primary"
        data-toggle="modal"
        data-target="#spa"
      >
        <Abrir />
      </button>
    </div>
  </div>

  <!-- Modal -->
  <div
    class="modal fade"
    id="spa"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-fullscreen">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">SPA</h5>
          <button
            type="button"
            class="btn-close"
            data-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Descrição</th>
                <th scope="col">Link</th>
                <th scope="col">Código Fonte</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <th scope="row">1</th>
                <td>
                  Mostra em um mapa os desastres e terremotos monitorados e disponibilizados através de APIs dos sites
                  <a href="https://reliefweb.int/" target="blank">ReliefWeb</a>
                  e 
                  <a href="https://earthquake.usgs.gov/" target="blank"
                    >usgs.gov</a
                  >
                </td>
                <td>
                  <a
                    href="https://albraga.github.io/spa-disaster-monitor-vuecli/"
                    target="blank"
                    >https://albraga.github.io/spa-disaster-monitor-vuecli/</a
                  >
                </td>
                <td>
                  <a
                    href="https://github.com/albraga/spa-disaster-monitor-vuecli"
                    target="blank"
                    >https://github.com/albraga/spa-disaster-monitor-vuecli</a
                  >
                </td>
              </tr>
              <tr>
                <th scope="row">2</th>
                <td>Portfólio pessoal</td>
                <td><a href="https://albraga.github.io/" target="blank">https://albraga.github.io/</a></td>
                <td><a href="https://github.com/albraga/albraga.github.io" target="blank">https://github.com/albraga/albraga.github.io</a></td>
              </tr>
               <tr>
                <th scope="row">3</th>
                <td>Projeto feito com tecnologia antiga</td>
                <td><a href="http://albraga.github.io/spa-cartomancy/" target="blank">http://albraga.github.io/spa-cartomancy</a></td>
                <td><a href="https://github.com/albraga/spa-cartomancy/" target="blank">https://github.com/albraga/spa-cartomancy</a></td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">
            Fechar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Abrir from "./Abrir.vue"
export default {
  components: {
    Abrir,
  },
}
</script>