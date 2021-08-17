<template>
  <div class="contain mt-5">
    <div class="row">
      <div class="col form-inline">
        <b-form-input
          v-model="newTask"
          placeholder="Добавить клиента"
          @keyup.enter="add"
        >
        </b-form-input>
        <b-button class="ml-3" variant="primary" @click="add"
          >Добавить</b-button
        >
      </div>
    </div>

    <div class="modal-window">
      <transition name="fade" appear>
        <div class="modal-overlay" v-if="!showModal">
          <div class="work-area">
            <div class="title-line">
              <h1 class="klient"></h1>
              <button class="close-modal" v-on:click="showModal = !showModal">
                x
              </button>
            </div>

            <div class="menu">
              <li v-for="point in arrayOfMenu" :key="point.item">
                {{ point.item }}
              </li>
            </div>
            <hr />
            <div class="main-container">
              <div class="l-1">
                <div class="general-section">
                  <h2>ОБЩИЙ РАЗДЕЛ</h2>
                  <hr />
                </div>
                <div class="contact-info">
                  <h2>КОНТАКТНАЯ ИНФОРМАЦИЯ</h2>
                  <hr />
                </div>
              </div>
              <div class="correspondence">
                <li v-for="point in arrayOfСorrespondence" :key="point.item">
                  {{ point.item }}
                </li>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>

    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 alert alert-secondary">
          <h1 class="">Новый</h1>
          <draggable
            class="list-group kanban-column"
            :list="arrBacklog"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-on:click="showModal = !showModal"
              v-for="element in arrBacklog"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-primary">
          <h1 class="">1-й контакт</h1>
          <draggable
            class="list-group kanban-column"
            :list="arrInProgress"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-on:click="showModal = !showModal"
              v-for="element in arrInProgress"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-warning">
          <h1 class="">Подбор авто</h1>
          <draggable
            class="list-group kanban-column"
            :list="arrTested"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-on:click="showModal = !showModal"
              v-for="element in arrTested"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h1 class="">Оформление договора</h1>
          <draggable
            class="list-group kanban-column"
            :list="Done"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-on:click="showModal = !showModal"
              v-for="element in Done"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "App",
  components: {
    draggable,
  },
  data() {
    return {
      showModal: true,
      newTask: "",
      arrBacklog: [
        { name: "Клиент 1" },
        { name: "Клиент 2" },
        { name: "Клиент 3" },
        { name: "Клиент 4" },
      ],
      arrInProgress: [],
      arrTested: [],
      Done: [],

      arrayOfMenu: [
        { item: "Общие" },
        { item: "Товары" },
        { item: "Предложения" },
        { item: "Работы" },
        { item: "Бизнес-процессы" },
        { item: "Связи" },
        { item: "История" },
        { item: "Шаблоны" },
        { item: "Супер звонки" },
        { item: "Приложения" },
      ],

      arrayOfСorrespondence: [
        { item: "Коментарий" },
        { item: "Ждать" },
        { item: "Звонок" },
        { item: "SMS" },
        { item: "Письмо" },
        { item: "Задача" },
        { item: "Встреча" },
        { item: "Визит" },
        { item: "Приложения" },
      ],
    };
  },
  methods: {
    add() {
      if (this.newTask) {
        this.arrBacklog.push({ name: this.newTask });
        this.newTask = "";
      }
    },
  },
};
</script>

<style>
@import "style-of-kanban.css";
@import "style-of-modal.css";
</style>
