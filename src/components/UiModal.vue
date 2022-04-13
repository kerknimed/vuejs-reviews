<template>
  <transition name="modal">
    <div class="ui-modal overlay component" v-if="show" @click="onClickOverlay" ref="overlay">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title font-weight-bold">New Review</h5>
            <button type="submit"  class="btn btn-primary font-weight-bold" @click="close" v-if="showCloseButton" disabled={}>Create</button>
          </div>
          <div class="modal-body">
            <form>
              <div class="form-group mt-1">
                <label for="reviewTypeSelect ">Review Type</label>
                <select class="form-control mt-2" id="reviewType" required>
                  <option>Maison Review</option>
                  <option>Quarterly Review</option>
                  <option>Yearly Review</option>
                </select>
              </div>
              <div class="form-group mt-3">
                <label for="yearlyReviewSelect ">Year</label>
                <select class="form-control mt-2" id="yearly-review" required>
                  <option>2022</option>
                  <option>2021</option>
                  <option>2020</option>
                </select>
              </div>
              <div class="form-group mt-3">
                <label for="quarterReviewSelect">Quarter</label>
                <select class="form-control mt-2" id="quarterly-review" required>
                  <option>Q1</option>
                  <option>Q2</option>
                  <option>Q3</option>
                  <option>Q4</option>
                </select>
              </div>
            </form>
          </div>
          <div class="modal-footer">
          </div>
        </div>
      </div>
      <!-- <span class="close" @click="close" v-if="showCloseButton">d,,d,qsdpos</span> -->
  </transition>
</template>

<script>
export default {
  name: 'UiModal',

  props: {
    show: {
      type: Boolean,
      default: false
    },
    showCloseButton: {
      type: Boolean,
      default: true
    },
    closeOnOverlay: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      listReviews: 'List Reviews',
      createReview: 'Create Review'
    }
  },

  methods: {
    close () {
      this.$emit('update:show', false)
    },
    onClickOverlay ($event) {
      if (this.closeOnOverlay && $event && $event.target === this.$refs.overlay) {
        this.close()
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.ui-modal.overlay.component {
  width: 100vw;
  height: 100vh;
  z-index: 100;
  position: fixed;
  top: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  .modal-content {
    width:40%;
    background-color: white;
    box-shadow: 0 7px 20px rgba(0, 0, 0, 0.5);
    .header {
      display: flex;
      justify-content: flex-end;
      .close {
        border: 1px solid black;
        padding: 2px;
        cursor: pointer;
      }
    }
  }
}

/* modal transition */
.modal-enter-active, .modal-leave-active {
  transition: all .3s ease;
}
.modal-enter, .modal-leave-to {
  padding-top: 100px;
  opacity: 0;
}
</style>
