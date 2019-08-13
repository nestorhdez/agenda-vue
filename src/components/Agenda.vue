<template>
    <div id="agenda">
        <div class="contact-form">
            <input v-model="newContact.name" @keyup="checkName" type="text" placeholder="Name...">
            <span class="error-text" v-if="!nameValid">{{nameValid ? '' : 'The name has to be longer than 6 characters.'}}</span>
            <input v-model="newContact.email" @keyup="checkEmail" type="text" placeholder="Email...">
            <span class="error-text" v-if="!emailValid">{{newContact.email == '' ? 'Email cannot be empty.' : 'This email already exists.'}}</span>
            <button :disabled="!emailValid || !nameValid" @click="addContact">Create new contact</button>
            <button @click="showCalleds">{{showAll ? 'Hide contacts I\'ve called' : 'Show contacts I\'ve called'}}</button>
            <button @click="checkAllCalled">Set all as called</button>
            <button @click="clearAll">Delete all contacts</button>
        </div>
        <Contacto @delete-contact="delContact($event)" v-bind:key="`c-${i}`" v-bind:contact="contact" v-for="(contact, i) in contactsFiltered"/>
    </div>
</template>

<script>
import Contacto from './Contacto.vue';
export default {
  name: 'Agenda',
  components: {
      Contacto
  },
  data() {
    return {
        newContact: {name: '', email: '', called: false, edit: false},
        contacts : [
            {name: 'Paco', email: 'paco@gmail.com', called: false, edit: false}
        ],
        nameValid: false,
        emailValid: false,
        showAll: false
    }
  },
  computed: {
        contactsFiltered() {
            if(this.showAll){
                return this.contacts;
            }else{
                return this.contacts.filter(c => !c.called);
            }
        }
  },
  methods : {
        addContact() {
            this.contacts.push({...this.newContact});
            this.newContact.name = '';
            this.newContact.email = '';
            this.nameValid = false;
            this.emailValid = false;
        },
        showCalleds() {
            this.showAll = !this.showAll;
        },
        checkName() {
            this.newContact.name.length > 6 ? this.nameValid = true : this.nameValid = false;
        },
        checkEmail() {
            if(this.contacts.map(c => c.email).find(email => email == this.newContact.email) || this.newContact.email === ''){
                this.emailValid = false;
            }else {
                this.emailValid = true;
            }
        },
        clearAll() {
            this.contacts = [];
        },
        checkAllCalled() {
            this.contacts.map(c => c.called = true);
        },
        delContact(email) {
            this.contacts = this.contacts.filter(c => c.email != email);
        }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#agenda {
    display: flex;
    flex-direction: column;
    background-color: white;
    color: #2c3e50;
    width: 450px;
    border-radius: 3px;
}
.error-text {
    color: tomato;
}
.contact-form {
    margin: 30px;
    display: flex;
    flex-direction: column;
    margin-bottom: 30px;
}
.contact-form * {
    margin: 5px 0;
}
</style>
