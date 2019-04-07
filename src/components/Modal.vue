<template>
  <!-- Modal -->
  <div class="modal fade" id="modalWindow" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalCenterTitle">{{local.modalwindow.title}}</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">{{local.modalwindow.message}}</div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="closeModalWindowForeve">{{local.modalwindow.buttoncloseforeve}}</button>
          <button type="button" class="btn btn-primary" data-dismiss="modal">{{local.modalwindow.buttonclose}}</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    local: Object
  },
  methods: {
    closeModalWindowForeve: function() {
      localStorage.setItem("showmodal", false);
    }
  }
};
</script>

<style scoped>
.modal-header .close:focus {
  outline: none;
}
.modal-content {
  border: none;
}
</style>
