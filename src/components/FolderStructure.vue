<template>
  <div class="container">
    <div class="outer-div">
      <span class="heading mdi mdi-chevron-down">Folder Structure</span>
      <div class="button-holder">
        <span
          class="icons mdi mdi-file-plus-outline"
          @click="openFileInput()"
        ></span>
        <span
          class="icons mdi mdi-folder-plus-outline"
          @click="openFolderInput()"
        ></span>
      </div>
    </div>
    <div class="file-folder-structure">
      <div v-for="(value, index) in sortData" :key="index">
        <FolderComponentVue
          :folderdata="value"
          :css="cssIndex"
          :isActive="true"
        />
      </div>

      <div class="mdi mdi-chevron-right" v-if="createFolderBool">
        <input
          type="text"
          ref="folderInput"
          v-model="folderName"
          @keyup.enter="createFolder"
        />
      </div>
      <div class="mdi mdi-file" v-if="createFileBool">
        <input
          type="text"
          ref="fileInput"
          v-model="fileName"
          @keyup.enter="createFile"
        />
      </div>
    </div>
  </div>
</template>
<script>
import FolderComponentVue from "./FolderComponent.vue";
export default {
  data() {
    return {
      data: [
        // {
        //   name: "Folder 1",
        //   type: "folder",
        //   subfolder: [
        //     {
        //       name: "Folder 3",
        //       type: "folder",
        //       subfolder: [
        //         { name: "15523", type: "file", subfolder: [], id: 6 },
        //         {
        //           name: "child",
        //           type: "folder",
        //           subfolder: [
        //             { name: "ssss", type: "folder", subfolder: [], id: 8 },
        //           ],
        //           id: 7,
        //         },
        //       ],
        //       id: 4,
        //     },
        //   ],
        //   id: 1,
        // },
        // {
        //   name: "Folder 2",
        //   type: "folder",
        //   subfolder: [{ name: "123", type: "file", subfolder: [], id: 5 }],
        //   id: 2,
        // },
        // { name: "File 1.txt", type: "file", subfolder: [], id: 3 },
      ],
      folderName: "",
      fileName: "",
      createFolderBool: false,
      createFileBool: false,
      active: {},
      folderToggle: false,
      counter: 1,
      showMenu: false,
      menuY: "",
      menuX: "",
      cssIndex: 0,
    };
  },
  components: {
    FolderComponentVue,
  },
  watch: {
    data: function (newData) {
      console.log(newData);
      this.$nextTick(() => {
        this.sortData;
      });
    },
  },
  computed: {
    sortData() {
      console.log('new', this.data);
      var temp = this.data;
      // temp.sort((a, b) => b.type.localeCompare(a.type));
      return temp;
    },
  },
  methods: {
    openFolderInput() {
      this.createFolderBool = true;
      this.$nextTick(() => {
        this.$refs.folderInput.focus();
        this.$refs.folderInput.addEventListener(
          "keydown",
          this.closeFolderInput
        );
      });
    },
    closeFolderInput(event) {
      if (event.keyCode === 27) {
        this.$refs.folderInput.removeEventListener(
          "keydown",
          this.closeFolderInput
        );
        this.createFolderBool = false;
      }
    },
    openFileInput() {
      this.createFileBool = true;
      this.$nextTick(() => {
        this.$refs.fileInput.focus();
        this.$refs.fileInput.addEventListener("keydown", this.closeFileInput);
      });
    },
    closeFileInput(event) {
      if (event.keyCode === 27) {
        this.$refs.fileInput.removeEventListener(
          "keydown",
          this.closeFileInput
        );
        this.createFileBool = false;
      }
    },
    createFolder() {
      var tempData = {
        name: this.folderName,
        type: "folder",
        subfolder: [],
        id: this.counter++,
      };
      this.data.push(tempData);
      console.log("0000000", this.data);

      this.folderName = "";
      this.createFolderBool = false;
    },
    createFile() {
      if (this.validateFileExtension()) {
        var tempData = {
          name: this.fileName,
          type: "file",
          subfolder: [],
          id: this.counter++,
        };
        this.data.push(tempData);

        this.fileName = "";
        this.createFileBool = false;
      } else {
        alert("Please enter a filename with a valid extension.");
      }
    },
    folderActive(folderData) {
      this.folderToggle = !this.folderToggle;
      var folderCss = document.getElementById(folderData.name);
      if (this.folderToggle) {
        this.active = folderData;
        folderCss.classList.remove("mdi-chevron-right");
        folderCss.classList.add("mdi-chevron-down");
        folderCss.style.backgroundColor = "#4F5669";
      } else {
        this.active = {};
        folderCss = document.getElementById(folderData.name);
        folderCss.classList.add("mdi-chevron-right");
        folderCss.classList.remove("mdi-chevron-down");
        folderCss.style.backgroundColor = "#20252c";
      }
    },
    showContextMenu(selectedFolder, event) {
      this.showMenu = false;
      event.preventDefault();
      this.active = selectedFolder;
      this.showMenu = true;
      this.menuX = event.pageX;
      this.menuY = event.pageY;
    },
    closeContextMenu() {
      this.showMenu = false;
    },
    validateFileExtension() {
      const filePath = this.fileName;
      const fileExtension = filePath.substring(filePath.lastIndexOf("."));
      if (/^[^.]*\.[^.]+[^.]*$/.test(fileExtension)) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
<style scoped>
.test {
  position: absolute;
  top: 100px;
  left: 20px;
  width: 400px;
}
.container {
  background-color: #272c35;
  color: white;
  height: 70vh;
  width: 30vw;
  text-align: left;
}
.context-menu {
  background-color: #272c35;
  border: 1px solid #3a404f;
  border-radius: 1px;
  width: 150px;
  position: absolute;
}
.outer-div {
  padding: 5px 0px;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
}
.heading {
  flex: 0 0 85%;
}
.button-holder {
  flex: 0 0 15%;
  font-size: 20px;
  display: flex;
  justify-content: space-between;
}
.file-folder-structure {
  background-color: #20252c;
  border: 1px solid #3a404f;
  border-radius: 1px;
  height: 62vh;
}
input[type="text"] {
  width: calc(100% - 16px);
  color: white;
  border: none;
  background-color: black;
}
.icons:hover {
  cursor: pointer;
}
.name-holder {
  width: 100%;
}
.folder-holder {
  display: flex;
}
</style>