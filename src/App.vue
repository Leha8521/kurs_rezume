<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="submitHandler">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="keyGroup">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model="textComent"></textarea>
      </div>
      <app-button color="primary" :disabled="textComent.length < 3">Добавить</app-button>
    </form>

    <div class="card card-w70">
      <div v-if="textGroup.length > 0">
        <component
          v-for="item in textGroup"
          :is="item.key"
          :dataText="item"
          :key="item.key"
        ></component>
      </div>
      <div v-else>
      <h3>Добавьте первый блок, чтобы увидеть результат</h3>
      </div>
    </div>
  </div>

<div class="container">
    <p>
      <app-button class="primary" @load="dounloadCont">Загрузить комментарии</app-button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item">
          <div>
            <p><strong>test@microsoft.com</strong></p>
            <small>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, reiciendis.</small>
          </div>
        </li>
      </ul>
    </div>
    <div class="loader"></div>
  </div>
</template>

<script>
import AppButton from './AppButton.vue'
import AppTitle from './AppTitle.vue'
import AppSubtitle from './AppSubtitle.vue'
import AppText from './AppText.vue'
import AppAvatar from './AppAvatar.vue'

export default {
  data () {
    return {
      keyGroup: 'title',
      textComent: '',
      textGroup: []
    }
  },
  methods: {
    submitHandler () {
      this.textGroup.push({
        key: 'app-' + this.keyGroup,
        text: this.textComent
      })
      this.keyGroup = 'title'
      this.textComent = ''
    },
    dounloadCont () {
      console.log('This is dounloadCont')
    }
  },
  components: { AppButton, AppTitle, AppSubtitle, AppText, AppAvatar }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
