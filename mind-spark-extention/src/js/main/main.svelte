<script lang="ts">
  import { onMount } from "svelte";
  import { os, path } from "../lib/cep/node";
  import {
    csi,
    evalES,
    evalTS,
    subscribeBackgroundColor
  } from "../lib/utils/bolt";

  import Header from "./components/Header.svelte";
  import Sidebar from "./components/Sidebar.svelte";

  import "../index.scss";
  import AddNote from "./components/AddNote/AddNote.svelte";
  import Chat from "./components/Chat/Chat.svelte";
  import EditNote from "./components/EditNote/EditNote.svelte";
  import Notes from "./components/Notes/Notes.svelte";
  import "./main.scss";

  let count: number = 0;
  let backgroundColor: string = "#282c34";

  //* Demonstration of Traditional string eval-based ExtendScript Interaction
  const jsxTest = () => {
    console.log(evalES(`helloWorld("${csi.getApplicationID()}")`));
  };

  //* Demonstration of End-to-End Type-safe ExtendScript Interaction
  const jsxTestTS = () => {
    evalTS("helloStr", "test").then((res) => {
      console.log(res);
    });
    evalTS("helloNum", 1000).then((res) => {
      console.log(typeof res, res);
    });
    evalTS("helloArrayStr", ["ddddd", "aaaaaa", "zzzzzzz"]).then((res) => {
      console.log(typeof res, res);
    });
    evalTS("helloObj", { height: 90, width: 100 }).then((res) => {
      console.log(typeof res, res);
      console.log(res.x);
      console.log(res.y);
    });
    evalTS("helloVoid").then(() => {
      console.log("function returning void complete");
    });
    evalTS("helloError", "test").catch((e) => {
      console.log("there was an error", e);
    });
  };

  const nodeTest = () => {
    alert(
      `Node.js ${process.version}\nPlatform: ${
        os.platform
      }\nFolder: ${path.basename(window.cep_node.global.__dirname)}`
    );
  };

  onMount(() => {
    if (window.cep) {
      subscribeBackgroundColor((c: string) => (backgroundColor = c));
    }
  });
</script>

<script lang='ts' context="module">
  enum TabNames {
    Notes = 'Notes',
    AddNote = 'AddNote',
    EditNote = 'EditNote',
    Chat = 'Chat'
  }


  type Note = {
    id: string;
    title: string;
    content: string | null;
    userId: string;
    createdAt: Date;
    updateAt: Date;
  }

  function hideAllTabs(){
    // change display style of the tabs to none
    
    const notes = document.querySelector('.notes-main') as HTMLElement;
    notes.style.display = "none";

    const addNotes = document.querySelector('.addNotes-main') as HTMLElement;
    addNotes.style.display = "none";

    const chat = document.querySelector('.chat-main') as HTMLElement;
    chat.style.display = "none";

    const edit = document.querySelector('.edit-main') as HTMLElement;
    edit.style.display = "none";
    
  }

  function edit_refresh() {
    const refreshBtn = document.getElementById('refresh-edit') as HTMLElement;
    refreshBtn.click();
  }
  function refresh() {
    const refreshBtn = document.getElementById('refresh') as HTMLElement;
    refreshBtn.click();
  }

  export var myNoteTitle:string;
  export const setMyNoteTitle = (value: string) => {
    myNoteTitle = value;
  }
  
  export var myNoteContent:string;
  export const setMyNoteContent = (value: string) => {
    myNoteContent = value;
  }
  
  export var myNote:Note;
  export const setMyNote = (note: Note) => {
    myNote = note;
  }

  export const navigate = (page: string) => {
    handleTabs(page)
  }

  
  export const token = import.meta.env.VITE_TOKEN
  export const userId = import.meta.env.VITE_UserId
  alert(userId)
  export const handleTabs = (tab : string, note?: Note) => {
    // evalTS("helloStr", tab).then((res) => {
    //   console.log(res);
    // });
    hideAllTabs()
    if (tab === "Home"){
      const nav = document.querySelector('.sidebar') as HTMLElement;
      //remove the :hidden" class from the nav
      nav.classList.add('hidden');
      // get the heafer with class app-header
      const header = document.querySelector('.app-header') as HTMLElement;
      //add the "hidden" class to the header
      header.classList.remove('hidden');
      const app = document.querySelector('.app') as HTMLElement;
      app.style.display = "block";

      const appMain = document.querySelector('.app-main') as HTMLElement;
      appMain.style.width = "auto";
      return;
    }
    // get the nav with class sidebar
    const nav = document.querySelector('.sidebar') as HTMLElement;
    //remove the :hidden" class from the nav
    nav.classList.remove('hidden');
    // get the heafer with class app-header
    const header = document.querySelector('.app-header') as HTMLElement;
    //add the "hidden" class to the header
    header.classList.add('hidden');
    const app = document.querySelector('.app') as HTMLElement;
    app.style.display = "flex";

    const appMain = document.querySelector('.app-main') as HTMLElement;
      appMain.style.width = "100%";
    // create a switch statement to handle the tabs
    switch(tab){
      case TabNames.Notes:
        hideAllTabs();
        refresh()
        const notes = document.querySelector('.notes-main') as HTMLElement;
        notes.style.display = "flex";
        break;
      case TabNames.AddNote:
        hideAllTabs();
        const addNotes = document.querySelector('.addNotes-main') as HTMLElement;
        addNotes.style.display = "flex";
        break;
      case TabNames.Chat:
        hideAllTabs();
        const chat = document.querySelector('.chat-main') as HTMLElement;
        chat.style.display = "flex";
        break;
      case TabNames.EditNote:
        hideAllTabs();
        edit_refresh()
        const edit = document.querySelector('.edit-main') as HTMLElement;
        edit.style.display = "flex";
        break;
      default:
        console.log("default");
    }
  }

</script>


<div class="app" >
  <Sidebar />
  <Header />
  <main class="app-main">
    <Notes/>
    <AddNote/>
    <Chat/>
    <EditNote/>
  </main>
</div>

<style>
</style>
