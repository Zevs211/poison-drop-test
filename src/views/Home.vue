<template>
  <div class="container">
    <div class="info">
      <div class="personal-info">
        <h2>Личная информация:</h2>
        <v-input
          placeholder="Фамилия"
          label="Фамилия"
          v-model="lName"
        />
        <v-input
          placeholder="Имя"
          label="Имя"
          v-model="fName"
        />
        <v-input
          placeholder="Email"
          label="Email"
          v-model="email"
        />
        <v-input
          placeholder="Телефон"
          label="Телефон"
          v-model="phone"
        />
        <div class="selectGender">
          <VCheckbox id="man" v-model="gender.man.isSelected" @input="onSelectGender(gender.man)"><p>{{gender.man.name}}</p></VCheckbox>
          <VCheckbox id="woman" v-model="gender.woman.isSelected" @input="onSelectGender(gender.woman)"><p>{{gender.woman.name}}</p></VCheckbox>
        </div>
      </div>
      <div>
        <h2>Информация о кандидате:</h2>
        <h3>Образование</h3>
        <div v-for="(item, index) in educationList" :key="index">
          <VCheckbox>{{item}}</VCheckbox>
        </div>
        <h3>Владение фреймворками</h3>
        <div v-for="(framework, index) in frameworksList" :key="index">
          <VCheckbox v-model="framework.isSelected" >{{framework}}</VCheckbox>
        </div>
        <h3>СМС оповещения</h3>
        <div class="sms">
          <div><VCheckbox>Отправлять</VCheckbox></div>
          <div class="not-send"><VCheckbox>Не отправлять</VCheckbox></div>
        </div>
      </div>
      <div>
        <h2>Опыт работы</h2>
        <v-input/>
      </div>
    </div>
    <button @click="submit">Press me</button>
  </div>
</template>

<script>
import VInput from '../components/VInput.vue';
import VCheckbox from '../components/VCheckbox.vue';

export default {
  components: {
    VInput,
    VCheckbox
  },
  data(){
    return{
      lName: '',
      fName: '',
      email: '',
      phone: '',
      educationList: ['Среднее', 'Средне-специальное', 'Неоконченное высшее', 'Бакалавр', 'Магистр', 'Аспирант'],
      frameworksList: ['Vue', 'React', 'Angular', 'Svelte', 'Ember.js'],
      gender: {
        man: {
          id: 0,
          name: "Мужской",
          isSelected: false,
        },
        woman: {
          id: 1,
          name: "Женский",
          isSelected: false,
        },
      },
    }
  },
  methods:{
    onSelectGender(value){
      if(value.id === 0){
        this.gender.man.isSelected = value.isSelected
        this.gender.woman.isSelected = value.isSelected
      } else if(value.id === 1){
        this.gender.woman.isSelected = value.isSelected
        this.gender.man.isSelected = value.isSelected
      }
    },
    submit(){
      const data = {
        frameworksList: this.frameworksList.filter(framework => framework.isSelected)
      }
      console.log(data);
    }
  }
}
</script>

<style scoped lang="scss">
  .container{
    width: 100%;
    height: 100%;
    .info{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      .personal-info{
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        .selectGender{
          display: flex;
          #woman{
            margin-left: 16px;
          }
        }
      }
      .sms{
        display: flex;
        .not-send{
          margin-left: 16px;
        }
      }
    }
  }
</style>