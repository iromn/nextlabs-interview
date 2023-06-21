<template>
  <div v-if="isActive">
    <!-- <div v-for="(value, index) in sortData" :key="index"> -->
    <div
      @contextmenu.stop="(event) => showContextMenu(folderData, event)"
      @click="closeContextMenu"
    >
      <div
        :style="`padding-left: calc(15 * ${css}px);`"
        class="name-holder icons mdi folder-holder"
        :class="
          Object.keys(folderData).length > 0
            ? folderData.type == 'folder'
              ? 'mdi-chevron-right'
              : 'mdi-file'
            : ''
        "
        :id="folderData.name"
        @click="folderActive(folderData)"
      >
        {{ folderData.name }}
      </div>
      <div v-for="(value, index) in folderData.subfolder" :key="index">
        <FolderComponent
          :folderdata="value"
          :css="cssIndex"
          :isActive="isSelected"
        />
      </div>
      <div
        :style="`padding-left: calc(15 * ${css + 1}px);`"
        class="mdi mdi-chevron-right"
        v-if="createFolderBool"
      >
        <input
          type="text"
          ref="folderInput"
          v-model="folderName"
          @keyup.enter="createFolder"
        />
      </div>
      <div
        :style="`padding-left: calc(15 * ${css}px);`"
        class="mdi mdi-chevron-right"
        v-if="editFolderBool"
      >
        <input
          type="text"
          ref="editInput"
          v-model="editName"
          @keyup.enter="editFolder"
        />
      </div>
    </div>
  </div>
  <!-- </div> -->
  <div
    v-if="showMenu"
    class="context-menu"
    :style="{ top: `${menuY}px`, left: `${menuX}px` }"
  >
    <div><label @click="createSubFolder">New Folder</label></div>
    <div><label>New File</label></div>
    <div><label @click="editSubFolder">Edit</label></div>
    <div><label @click="deleteFolder">Delete</label></div>
  </div>
</template>
<script>
export default {
  name: "FolderComponent",
  props: {
    folderdata: Object,
    css: Number,
    isActive: Boolean,
  },
  data() {
    return {
      folderData: this.folderdata,
      folderToggle: false,
      //   cssIndex: 0,
      isSelected: false,
      active: {},
      showMenu: false,
      menuY: "",
      menuX: "",
      folderName: "",
      createFolderBool: false,
      editFolderBool: false,
      cssIndex: this.css + 1,
      editName: this.folderdata.name,
    };
  },
  computed: {
    sortData() {
      var temp = this.folderData;
      temp.sort((a, b) => b.type.localeCompare(a.type));
      return temp;
    },
  },
  methods: {
    folderActive(element) {
      if (element.type == "folder") {
        this.folderToggle = !this.folderToggle;
        var folderCss = document.getElementById(element.name);
        if (this.folderToggle) {
          this.isSelected = true;
          this.active = element;
          folderCss.classList.remove("mdi-chevron-right");
          folderCss.classList.add("mdi-chevron-down");
          folderCss.style.backgroundColor = "#4F5669";
        } else {
          this.active = {};
          this.isSelected = false;
          folderCss = document.getElementById(element.name);
          folderCss.classList.add("mdi-chevron-right");
          folderCss.classList.remove("mdi-chevron-down");
          folderCss.style.backgroundColor = "#20252c";
        }
      } else {
        return;
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
    createSubFolder() {
      this.createFolderBool = true;
      this.closeContextMenu();
      this.$nextTick(() => {
        this.$refs.folderInput.focus();
      });
    },
    editSubFolder() {
      this.editName = this.folderData.name;
      this.editFolderBool = true;
      this.closeContextMenu();
    },
    createFolder() {
      var tempData = {
        name: this.folderName,
        type: "folder",
        subfolder: [],
        id: this.folderData.index++,
      };
      this.folderData = {
        ...this.folderData,
        subfolder: [...this.folderData.subfolder, tempData],
      };
      this.folderName = "";
      this.createFolderBool = false;
    },
    deleteFolder() {
      this.folderData = {};
      this.folderName = "";
      this.createFolderBool = false;
    },
    editFolder() {
      this.folderData.name = this.editName;
      this.editName = "";
      this.editFolderBool = false;
    },
  },
};
</script>
<style scoped>
.icons:hover {
  cursor: pointer;
}
.name-holder {
  width: 100%;
}
.folder-holder {
  display: flex;
}
.context-menu {
  background-color: #272c35;
  border: 1px solid #3a404f;
  border-radius: 1px;
  width: 150px;
  position: absolute;
}
input[type="text"] {
  width: calc(100% - 16px);
  color: white;
  border: none;
  background-color: black;
}
</style>