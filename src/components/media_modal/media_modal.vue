<template>
  <Modal
    v-if="showing"
    class="media-modal-view"
    @backdropClicked="hide"
  >
    <img
      v-if="type === 'image'"
      class="modal-image"
      :src="currentMedia.url"
      @touchstart.stop="mediaTouchStart"
      @touchmove.stop="mediaTouchMove"
    >
    <VideoAttachment
      v-if="type === 'video'"
      class="modal-image"
      :attachment="currentMedia"
      :controls="true"
      @click.stop.native=""
    />
    <button
      v-if="canNavigate"
      :title="$t('media_modal.previous')"
      class="modal-view-button-arrow modal-view-button-arrow--prev"
      @click.stop.prevent="goPrev"
    >
      <i class="icon-left-open arrow-icon" />
    </button>
    <button
      v-if="canNavigate"
      :title="$t('media_modal.next')"
      class="modal-view-button-arrow modal-view-button-arrow--next"
      @click.stop.prevent="goNext"
    >
      <i class="icon-right-open arrow-icon" />
    </button>
  </Modal>
</template>

<script src="./media_modal.js"></script>

<style lang="scss">
.modal-view.media-modal-view {
  z-index: 1001;

  .modal-view-button-arrow {
    opacity: 0.75;

    &:focus,
    &:hover {
      outline: none;
      box-shadow: none;
    }
    &:hover {
      opacity: 1;
    }
  }
}

.modal-image {
  max-width: 90%;
  max-height: 90%;
  box-shadow: 0px 5px 15px 0 rgba(0, 0, 0, 0.5);
  image-orientation: from-image; // NOTE: only FF supports this
}

.modal-view-button-arrow {
  position: absolute;
  display: block;
  top: 50%;
  margin-top: -50px;
  width: 70px;
  height: 100px;
  border: 0;
  padding: 0;
  opacity: 0;
  box-shadow: none;
  background: none;
  appearance: none;
  overflow: visible;
  cursor: pointer;
  transition: opacity 333ms cubic-bezier(.4,0,.22,1);

  .arrow-icon {
    position: absolute;
    top: 35px;
    height: 30px;
    width: 32px;
    font-size: 14px;
    line-height: 30px;
    color: #FFF;
    text-align: center;
    background-color: rgba(0,0,0,.3);
  }

  &--prev {
    left: 0;
    .arrow-icon {
      left: 6px;
    }
  }

  &--next {
    right: 0;
    .arrow-icon {
      right: 6px;
    }
  }
}
</style>
