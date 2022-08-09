<template>
  <v-app>
    <v-main
        @dragover.prevent="drag = true"
        @dragleave.prevent="drag = false"
        class="window_area"
        @drop.prevent="onWindowDrop"
    >
      <div>
        <div
            class="image-input__field"
            v-bind:class="{  'image-input__field_false': !canDrag }"
            @dragover.prevent="drag = true"
            @dragleave.prevent="drag = false"
            @drop.prevent="onDrop"
        >
          <p>画像をドラッグ＆ドロップ <br />またはクリックでファイル選択</p>
        </div>
        <div v-if="file">
          ファイル名： {{ file.name }}
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'App',
  components: {

  },
  methods:{
    onDrop(event:any) {
      if(!this.canDrag)
      {
        return;
      }

      this.isDragOver = false;
      const files = event.dataTransfer.files;
      if (files.length !== 1 || files[0].type.indexOf("image") !== 0) {
        return;
      }
      this.file = (event.dataTransfer as DataTransfer).files[0]
      this.canDrag = false;
      setTimeout(() =>
      {
        this.canDrag = true;
      }, 2000)
    },
    onWindowDrop(event:any){
      event.preventDefault();
    },
  },

  data () {
    return {
      //
      isDragOver:true as boolean,
      drag:false as boolean,
      file:null as File | null,
      canDrag : true as boolean
    }
  },
})
</script>

<style>
.image-input__field {
  width: 500px;
  height: 300px;
  border: 2px solid gray;
  border-radius: 15px;
  padding: 20px;
  margin: 30px;
}
.image-input__field_false {
  width: 500px;
  height: 300px;
  border: 2px solid lightgray;
  border-radius: 15px;
  padding: 20px;
  margin: 30px;
  color: lightgray;
}
.window_area{
  background: lightcyan;
}
</style>
