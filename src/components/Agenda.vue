<template>
    <div id="agenda">
        <div class="contact-form">
            <input v-model="newContact.name" @keyup="checkName" type="text" placeholder="Name...">
            <span v-if="!nameValid">{{nameValid ? '' : 'The name has to be longer than 6 characters.'}}</span>
            <input v-model="newContact.email" @keyup="checkEmail" type="text" placeholder="Email...">
            <span v-if="!emailValid">{{newContact.email == '' ? 'Email cannot be empty.' : 'This email already exists.'}}</span>
            <button :disabled="!emailValid || !nameValid" @click="addContact">Create new contact</button>
            <button @click="showCalleds">Show contacts I've called</button>
            <button @click="checkAllCalled">Set all as called</button>
            <button @click="clearAll">Delete all contacts</button>
        </div>
        <div v-bind:key="`c-${index}`" class="contact" v-for="(contact, index) in contacts.filter(contact => !contact.called)">
            <button @click="contact.called = true" class="btn btn--called">Called</button>
            <button @click="toggleEditContact(contact)" class="btn btn--edit">Edit</button>
            <button @click="delContact(contact.email)" class="btn btn--delete">Delete</button>
            <h2 :contenteditable="contact.edit" :class="{'editable' : contact.edit}" class="name">{{contact.name}}</h2>
            <h3 :contenteditable="contact.edit" :class="{'editable' : contact.edit}" class="email">{{contact.email}}</h3>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Agenda',
  data() {
    return {
        newContact: {name: '', email: '', called: false, edit: false},
        contacts : [
            {name: 'Paco', email: 'paco@gmail.com', called: false, edit: false}
        ],
        nameValid: false,
        emailValid: false
    }
  },
  methods : {
        addContact() {
            this.contacts.push({...this.newContact});
            this.newContact.name = '';
            this.newContact.email = '';
            this.nameValid = false;
            this.emailValid = true;
        },
        delContact(cToDel) {
            this.contacts = this.contacts.filter(contact => contact.email != cToDel);
        },
        toggleEditContact(contact) {
            contact.edit = !contact.edit;
        },
        showCalleds() {
            let calleds = this.contacts.filter(c => c.called).forEach(c => c.called = false);
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
.contact-form {
    margin: 30px;
    display: flex;
    flex-direction: column;
    margin-bottom: 30px;
}
.contact-form * {
    margin: 5px 0;
}
.contact {
    border-top: 1px solid #2c3e50;
    display: inline-block;
    width: 100%;
    padding: 10px 20px;
    text-align: left;
}
.contact h3 {
    margin: 5px 0;
}
.contact h2, .contact h3 {
    width: 80%;
}
.editable {
    border: 1px solid green;
}
.contact input {
    display: block;
    margin: 10px 0;
}
.btn {
    margin-right: 5px;
    border-radius: 5px;
    border-width: 1px;
    background-color: white;
    padding: 2px 5px;
}
.btn--delete {
    background-color: red;
    color: white;
}
.name {
    margin: 10px 0;
}
.red {
    border: 1px solid red;
}
</style>
