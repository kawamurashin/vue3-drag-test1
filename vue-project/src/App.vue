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
      this.isDragOver = false;
      const files = event.dataTransfer.files;
      if (files.length !== 1 || files[0].type.indexOf("image") !== 0) {
        return;
      }
      this.file = (event.dataTransfer as DataTransfer).files[0]
    },
    onWindowDrop(event:any){
      event.preventDefault();
    }
  },

  data () {
    return {
      //
      isDragOver:true as boolean,
      drag:false as boolean,
      file:null as File | null
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
.window_area{
  background: lightcyan;
}
</style>
