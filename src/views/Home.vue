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
          <VRadioGroup :items="gender" v-model="selectGender"></VRadioGroup>
        </div>
      </div>
      <div>
        <h2>Информация о кандидате:</h2>
        <h3>Образование</h3>
        <VRadioGroup :items="educationList" v-model="education"></VRadioGroup>
        <h3>Владение фреймворками</h3>
        <div v-for="framework in frameworksList" :key="framework.id">
          <VCheckbox :value="framework.isSelected" @input="onSelectFramework(framework)">{{framework.name}}</VCheckbox>
        </div>
        <h3>SMS оповещения</h3>
        <VRadioGroup :items="sms" v-model="message"></VRadioGroup>
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
import VRadioGroup from '../components/VRadioGroup.vue';

export default {
  components: {
    VInput,
    VCheckbox,
    VRadioGroup
},
  data(){
    return{
      message: '',
      education: '',
      selectGender:'',
      lName: '',
      fName: '',
      email: '',
      phone: '',
      educationList: [
        {
          id: 0,
          name: 'Среднее',
          isSelected: false
        },
        {
          id: 1,
          name: 'Средне-специальное',
          isSelected: false
        },
        {
          id: 2,
          name: 'Неоконченное высшее',
          isSelected: false
        },
        {
          id: 3,
          name: 'Бакалавр',
          isSelected: false
        },
        {
          id: 4,
          name: 'Магистр',
          isSelected: false
        },
        {
          id: 5,
          name: 'Аспирант',
          isSelected: false
        }
      ],
      frameworksList: [
        {
          id: 0,
          name: 'Vue',
          isSelected: false
        },
        {
          id: 1,
          name: 'React',
          isSelected: false
        },
        {
          id: 2,
          name: 'Angular',
          isSelected: false
        },
        {
          id: 3,
          name: 'Svelte',
          isSelected: false
        },
        {
          id: 4,
          name: 'Ember',
          isSelected: false
        }
      ],
      gender:[
        {
          id: 0,
          name: "Мужской",
          isSelected: false,
        },
        {
          id: 1,
          name: "Женский",
          isSelected: false,
        }
      ],
      sms:[
        {
          id: 0,
          name: 'Отправлять',
          isSelected: false
        },
        {
          id: 1,
          name: 'Не отпралять',
          isSelected: false
        }
      ]     
    }
  },
  methods:{
    radioSelector(item){
      console.log(item);
      const educations = this.educationList.map((education) => {
        if(education.id === item){
          education.isSelected = true
        } else education.isSelected = false
      })
      this.educationList = educations
      console.log(this.educationList);
    },
    onSelectFramework(item){
      this.frameworksList.forEach((el) => {
        if(item.id === el.id){el.isSelected = !el.isSelected}
      })
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
          justify-content: space-between;
          margin-top: 16px;
        }
      }
      .education{
        display: flex;
        align-items: center;
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