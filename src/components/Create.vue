<template>
  <div class="wrapper">
    <img src="@/assets/img_267727.png" class="close">
    <input v-model="label" placeholder="Название..." type="text">
    <input v-model="description" placeholder="Описание..." type="text">
    <hr>
    <h3>Выберите участников чата.</h3>
    <div class="addMemberWrapper">
      <input v-model="selectMember" placeholder="Выберите участника..." type="text">
      <div v-on:click="add_member_button_handler" class="addMemberButton button">Добавить</div>
    </div>
    <div class="addedMembersList">
      Добавленные участники:
    </div>
    <div v-on:click="create_chat_button_handler" class="submit button">Создать</div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  serverUrl: 'http://195.49.210.34/',
  name: 'CreateChat',
  data: ()=>({
    label:'',
    description:'',
    selectMember: '',
    selectedMembers: [],
  }),
  methods:{

    create_chat_button_handler: async function (){
      console.log(this.$route.params.id)
      if(!this.label) return alert()
      if(!this.description) return alert()
      if(!this.description) return alert()
      if(!this.selectedMembers.length <=0) return alert()

      const data_for_create_chat = {
        label: this.label,
        description: this.description,
        userId: this.$route.params.id,
        members: this.selectMember
      }

      const response = await this.sendRequest('chat/create','POST',data_for_create_chat)
      if(response.info.status === 'Error') return alert(response.payload)

      return alert(`Чат ${this.label}, успешно создан`)
    },
    add_member_button_handler: async function (){
      if(!this.selectMember) return alert ('Вы не выбрали участника')
      if(this.this.selectedMembers.includes(this.selectMember)) return alert("Вы уже выбрали этого участника")

      this.selectedMembers.push(selectMember)
      this.selectMember = ''
    },
    sendRequest: async function(path, method, body) {
                const url = `${this.serverUrl}${path}`;
                let response;

                method = method.toLowerCase();

                return (await axios[method](url, body)).data;

            }, 
  }
}
</script>

<style scoped lang="less">
  .wrapper {
    width: 50vw;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    position: relative;
    padding-top: 50px;
    border: 1px solid rgba(37, 47, 37, 1);
    padding: 20px;
    border-radius: 10px;
    .close {
      width: 2.5%;
      position: absolute;
      right: 5px;
      top: 5px;
      cursor: pointer;
      margin: 0;
    }
    .addMemberWrapper {
      width: 50%;
      display: flex;
      justify-content: space-evenly;
      align-items: center;
      input {
        width: 60%;
      }
    }
    .button {
      padding: 4px 16px;
      border: 1px solid rgba(37, 47, 37, 1);
      border-radius: 10px;
      cursor: pointer;
    }
    input {
      width: 40%;
      padding: 8px 16px;
      outline: none;
      border: 1px solid rgba(37, 47, 37, 1);
      border-radius: 10px;
    }
    * {
      margin-top: 20px;
    }
    hr {
      width: 100%;
    }
    h3 {
      padding: 0;
      margin: 0;
    }
  }
</style>