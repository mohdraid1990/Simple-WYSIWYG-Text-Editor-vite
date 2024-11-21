<template>
  <div class="editor-container">
    <!-- Toolbar Buttons -->
    <div class="toolbar">
      <button @click="undo">
        <img src="./assets/arrow-down.svg" alt="Undo" />
      </button>
      <button @click="redo">
        <img src="./assets/arrowup.svg" alt="Redo" />
      </button>
      <button @click="format('h1')">
        <img src="./assets/H1.svg" alt="Heading 1" />
      </button>
      <button @click="format('p')">
        <img src="./assets/text.svg" alt="Paragraph" />
      </button>
      <button @click="insertImage">
        <img src="./assets/photo.svg" alt="Insert Image" />
      </button>
      <a @click="copyHTML">Скопировать HTML</a>
    </div>
    <!-- Editable Content Area -->
    <div class="editor" ref="editor" contenteditable="true">
      <p>
        Таким образом консультация с широким активом представляет собой
        интересный эксперимент проверки позиций, занимаемых участниками в
        отношении поставленных задач. С другой стороны постоянное
        информационно-пропагандистское обеспечение нашей деятельности
        представляет собой интересный эксперимент проверки форм развития.
        Идейные соображения высшего порядка, а также укрепление и развитие
        структуры влечет за собой процесс внедрения и модернизации
        соответствующий условий активизации. Задача организации, в особенности
        же реализация намеченных плановых заданий играет важную роль в
        формировании дальнейших направлений развития. Повседневная практика
        показывает, что постоянное <br />
        информационно-пропагандистское обеспечение нашей деятельности играет
        важную роль в формировании существенных финансовых и административных
        условий.
      </p>
      <!-- Default Content -->
      <h1>Смотрите какие обезьянки</h1>
      <img src="./assets/image 1.png" alt="#" />
      <p>
        Таким образом консультация с широким активом представляет собой
        интересный <br />
        эксперимент проверки позиций, занимаемых участниками в отношении
        поставленных задач. С другой стороны постоянное
        информационно-пропагандистское обеспечение нашей деятельности
        представляет собой инйцу шо шщйоц ущойц ущошцщйуо йцщуо йщцоу щйоу
        шщйцош ущйтересный эксперимент проверки форм развития. Идейные
        соображения высшего порядка, а также укрепление и развитие структуры
        влечет за собой процесс внедрения и модернизации соответствующий условий
        активизации. Задача организации, в особенности же реализация намеченных
        плановых заданий <br />
        играет важную роль в формировании дальнейших направлений развития.
        <br />
        Повседневная практика показывает, что постоянное <br />
        информационно-пропагандистское обеспечение нашей деятельности играет
        важную роль в формировании существенных финансовых и административных
        условий.
      </p>
      <p>
        Товарищи! новая модель организационной деятельности требуют от нас
        анализа направлений прогрессивного развития. Задача организации, в
        особенности же постоянный количественный рост и сфера нашей активности
        требуют от нас анализа позиций, занимаемых участниками в отношении
        поставленных задач. Задача организации, в особенности же реализация
        намеченных плановых заданий требуют от нас анализа системы обучения
        кадров, соответствует насущным потребностям.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      history: [],
      historyIndex: -1,
    };
  },
  methods: {
    saveHistory() {
      const content = this.$refs.editor.innerHTML;
      if (this.historyIndex === -1 || this.history[this.historyIndex] !== content) {
        this.history.splice(this.historyIndex + 1);
        this.history.push(content);
        this.historyIndex++;
      }
    },
    undo() {
      if (this.historyIndex > 0) {
        this.historyIndex--;
        this.$refs.editor.innerHTML = this.history[this.historyIndex];
      }
    },
    redo() {
      if (this.historyIndex < this.history.length - 1) {
        this.historyIndex++;
        this.$refs.editor.innerHTML = this.history[this.historyIndex];
      }
    },
    format(tag) {
      document.execCommand("formatBlock", false, `<${tag}>`);
      this.saveHistory();
    },
    insertImage() {
      const imageUrl = prompt("Enter image URL:");
      if (imageUrl) {
        const img = document.createElement('img');
        img.src = imageUrl;
        img.alt = 'Inserted Image';
        this.$refs.editor.appendChild(img);
        this.saveHistory();
      }
    },
    copyHTML() {
      const html = this.$refs.editor.innerHTML;
      navigator.clipboard.writeText(html).then(() => {
        alert("HTML copied to clipboard!");
      });
    }
  },
  mounted() {
    this.saveHistory();
    this.$refs.editor.addEventListener("input", this.saveHistory);
  },
};
</script>

<style>
body {
  background-color: #080808;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  height: 200vh;
}
.editor-container {
  padding: 20px;
  display: flex;
  flex-direction: column;
}
.toolbar {
  display: flex;
  gap: 10px;
  align-items: center;
  padding-left: 10px;
}
.toolbar button {
  padding: 10px;
  border: none;
  background-color: #282828;
  color: #fff;
  width: 42px;
  height: 38px;
  text-align: center;
  cursor: pointer;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.toolbar button:hover {
  background-color: #0056b3;
}
.editor {
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 20px;
}
.editor p {
  font-family: Roboto;
  font-size: 15px;
  font-weight: 400;
  line-height: 23px;
  text-align: left;
  text-underline-position: from-font;
  text-decoration-skip-ink: none;
  width: 621px;
  height: 253px;
}
.editor p:nth-of-type(2) {
  font-family: Roboto;
  font-size: 15px;
  font-weight: 400;
  line-height: 23px;
  text-align: left;
  text-underline-position: from-font;
  text-decoration-skip-ink: none;
}
.editor p:nth-of-type(3) {
  padding: 10px;
}
.large-text {
  font-size: 20px;
  line-height: 28px;
  margin-bottom: 30px;
}
</style>
