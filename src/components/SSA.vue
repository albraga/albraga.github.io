<template>
    <div class="card">
            <h5 class="card-header">SSA</h5>
            <div class="card-body">
              <h5 class="card-title">Server-Side Application</h5>
              <p class="card-text">
                 Projetos criados com <a href="https://nodejs.org/pt-br/">Node.js</a> e diversos outros recursos.
              </p>
              <!-- Button trigger modal -->
              <button
                type="button"
                class="btn btn-primary"
                data-toggle="modal"
                data-target="#exampleModal"
              >
              <Abrir />
              </button>
            </div>
          </div>

          <!-- Modal -->
          <div
            class="modal fade"
            id="exampleModal"
            tabindex="-1"
            aria-labelledby="exampleModalLabel"
            aria-hidden="true"
          >
            <div class="modal-dialog modal-fullscreen">
              <div class="modal-content">
                <div class="modal-header">
                  <h5 class="modal-title" id="exampleModalLabel">
                    Modal title
                  </h5>
                  <button
                    type="button"
                    class="btn-close"
                    data-dismiss="modal"
                    aria-label="Close"
                  ></button>
                </div>
                <div class="modal-body">
                  Cras mattis consectetur purus sit amet fermentum. Cras justo
                  odio, dapibus ac facilisis in, egestas eget quam. Morbi leo
                  risus, porta ac consectetur ac, vestibulum at eros. Praesent
                  commodo cursus magna, vel scelerisque nisl consectetur et.
                  Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor
                  auctor. Aenean lacinia bibendum nulla sed consectetur.
                  Praesent commodo cursus magna, vel scelerisque nisl
                  consectetur et. Donec sed odio dui. Donec ullamcorper nulla
                  non metus auctor fringilla. Cras mattis consectetur purus sit
                  amet fermentum. Cras justo odio, dapibus ac facilisis in,
                  egestas eget quam. Morbi leo risus, porta ac consectetur ac,
                  vestibulum at eros. Praesent commodo cursus magna, vel
                  scelerisque nisl consectetur et. Vivamus sagittis lacus vel
                  augue laoreet rutrum faucibus dolor auctor. Aenean lacinia
                  bibendum nulla sed consectetur. Praesent commodo cursus magna,
                  vel scelerisque nisl consectetur et. Donec sed odio dui. Donec
                  ullamcorper nulla non metus auctor fringilla. Cras mattis
                  consectetur purus sit amet fermentum. Cras justo odio, dapibus
                  ac facilisis in, egestas eget quam. Morbi leo risus, porta ac
                  consectetur ac, vestibulum at eros. Praesent commodo cursus
                  magna, vel scelerisque nisl consectetur et. Vivamus sagittis
                  lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean
                  lacinia bibendum nulla sed consectetur. Praesent commodo
                  cursus magna, vel scelerisque nisl consectetur et. Donec sed
                  odio dui. Donec ullamcorper nulla non metus auctor fringilla.
                  Cras mattis consectetur purus sit amet fermentum. Cras justo
                  odio, dapibus ac facilisis in, egestas eget quam. Morbi leo
                  risus, porta ac consectetur ac, vestibulum at eros. Praesent
                  commodo cursus magna, vel scelerisque nisl consectetur et.
                  Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor
                  auctor. Aenean lacinia bibendum nulla sed consectetur.
                  Praesent commodo cursus magna, vel scelerisque nisl
                  consectetur et. Donec sed odio dui. Donec ullamcorper nulla
                  non metus auctor fringilla. Cras mattis consectetur purus sit
                  amet fermentum. Cras justo odio, dapibus ac facilisis in,
                  egestas eget quam. Morbi leo risus, porta ac consectetur ac,
                  vestibulum at eros. Praesent commodo cursus magna, vel
                  scelerisque nisl consectetur et. Vivamus sagittis lacus vel
                  augue laoreet rutrum faucibus dolor auctor. Aenean lacinia
                  bibendum nulla sed consectetur. Praesent commodo cursus magna,
                  vel scelerisque nisl consectetur et. Donec sed odio dui. Donec
                  ullamcorper nulla non metus auctor fringilla. Cras mattis
                  consectetur purus sit amet fermentum. Cras justo odio, dapibus
                  ac facilisis in, egestas eget quam. Morbi leo risus, porta ac
                  consectetur ac, vestibulum at eros. Praesent commodo cursus
                  magna, vel scelerisque nisl consectetur et. Vivamus sagittis
                  lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean
                  lacinia bibendum nulla sed consectetur. Praesent commodo
                  cursus magna, vel scelerisque nisl consectetur et. Donec sed
                  odio dui. Donec ullamcorper nulla non metus auctor fringilla.
                </div>
                <div class="modal-footer">
                  <button
                    type="button"
                    class="btn btn-secondary"
                    data-dismiss="modal"
                  >
                    Fechar
                  </button>
                </div>
              </div>
            </div>
          </div>
</template>

<script>
import Abrir from './Abrir.vue'
export default {
    components: {
      Abrir
    }
}
</script>