<template>
  <q-page class="page-container">
    <div class="b-container">
      <div class="row">
        <div class="col-6">
          <div
            @dragenter="onDragEnter"
            @dragleave="onDragLeave"
            @dragover="onDragOver"
            @drop="onDrop"
            class="drag-target rounded-borders overflow-hidden"
          >
            <img
              id="box1"
              style="max-width: 50px;"
              :src="require('assets/img_1.svg')"
              draggable="true"
              @dragstart="onDragStart"
            />
          </div>
        </div>

        <div class="col-6">
          <div
            @dragenter="onDragEnter"
            @dragleave="onDragLeave"
            @dragover="onDragOver"
            @drop="onDrop"
            class="drag-target justify-end rounded-borders overflow-hidden"
          >
            <img
              id="box2"
              style="max-width: 50px;"
              :src="require('assets/img_2.svg')"
              draggable="true"
              @dragstart="onDragStart"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="b-container minimized">
      <div class="row">
        <div class="col-12 q-my-md">
          <div class="row">
            <q-img
              :src="require('assets/rect_A.svg')"
              @dragenter="onDragEnter"
              @dragleave="onDragLeave"
              @dragover="onDragOver"
              @drop="onDrop"
              class="col-6 drop-target box overflow-hidden"
            />

            <q-img
              :src="require('assets/rect_B.svg')"
              @dragenter="onDragEnter"
              @dragleave="onDragLeave"
              @dragover="onDragOver"
              @drop="onDrop"
              class="col-6 drop-target box overflow-hidden"
            />

            <q-img
              :src="require('assets/rect_C.svg')"
              @dragenter="onDragEnter"
              @dragleave="onDragLeave"
              @dragover="onDragOver"
              @drop="onDrop"
              class="col-6 drop-target box overflow-hidden"
            />

            <q-img
              :src="require('assets/rect_D.svg')"
              @dragenter="onDragEnter"
              @dragleave="onDragLeave"
              @dragover="onDragOver"
              @drop="onDrop"
              class="col-6 drop-target box overflow-hidden"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="b-container">
      <div class="row">
        <div class="col-6">
          <div
            @dragenter="onDragEnter"
            @dragleave="onDragLeave"
            @dragover="onDragOver"
            @drop="onDrop"
            class="drag-target rounded-borders overflow-hidden"
          >
            <img
              id="box3"
              style="max-width: 50px;"
              :src="require('assets/img_3.svg')"
              draggable="true"
              @dragstart="onDragStart"
            />
          </div>
        </div>

        <div class="col-6">
          <div
            @dragenter="onDragEnter"
            @dragleave="onDragLeave"
            @dragover="onDragOver"
            @drop="onDrop"
            class="drag-target justify-end rounded-borders overflow-hidden"
          >
            <img
              id="box4"
              style="max-width: 50px;"
              :src="require('assets/img_4.svg')"
              draggable="true"
              @dragstart="onDragStart"
            />
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  methods: {
    // store the id of the draggable element
    onDragStart(e) {
      e.dataTransfer.setData('text', e.target.id);
      e.dataTransfer.dropEffect = 'move';
    },

    onDragEnter(e) {
      // don't drop on other draggables
      if (e.target.draggable !== true) {
        e.target.classList.add('drag-enter');

        if (e.target.children.length > 0) {
          e.target.classList.add('not-allowed');
        }
      }
    },

    onDragLeave(e) {
      // Set default borders
      e.target.classList.remove('drag-enter');
      e.target.classList.remove('not-allowed');
    },

    onDragOver(e) {
      e.preventDefault();
    },

    onDrop(e) {
      e.preventDefault();

      // don't drop on other draggables
      if (e.target.draggable === true) {
        return;
      }

      const draggedId = e.dataTransfer.getData('text');
      const draggedEl = document.getElementById(draggedId);

      // check if original parent node
      if (draggedEl.parentNode === e.target) {
        e.target.classList.remove('drag-enter');
        return;
      }

      // Check if box is not available
      if (e.target.children.length < 1) {
        // make the exchange
        draggedEl.parentNode.removeChild(draggedEl);
        e.target.appendChild(draggedEl);
      }

      // Set default borders if has
      e.target.classList.remove('drag-enter');
      e.target.classList.remove('not-allowed');
    },
  },
};
</script>

<style lang="scss">
.page-container {
  padding-top: 20vh;
  height: 100vh;
}

.b-container {
  width: 100%;
  max-width: 420px;
  margin: 0 auto;

  &.minimized {
    max-width: 250px;
  }
}

.box {
  display: flex;
  align-items: center;
  justify-content: center;
}

.drag-target {
  cursor: pointer;
  border: 2px solid transparent;
  min-height: 60px;
  display: flex;
  align-items: center;
}

.drop-target {
  border: 2px solid transparent;

  .q-img__content {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

.drag-enter {
  border: 3px dashed $light-green-13;

  &.not-allowed {
    border: 3px dashed $red;
  }
}
</style>
