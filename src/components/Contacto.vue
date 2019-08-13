<template>
  <div class="contact" :class="{'called' : contact.called}">
        <button @click="contact.called = !contact.called" class="btn btn--called">Called</button>
        <button @click="toggleEditContact(contact)" class="btn btn--edit">Edit</button>
        <button @click="$emit('delete-contact', contact.email)" class="btn btn--delete">Delete</button>
        <h2 :contenteditable="contact.edit" :class="{'editable' : contact.edit}" class="name">{{contact.name}}</h2>
        <h3 :contenteditable="contact.edit" :class="{'editable' : contact.edit}" class="email">{{contact.email}}</h3>
    </div>
</template>

<script>
export default {
    name: 'Contacto',
    props: {
        contact: {
            name : String,
            email : String,
            called : Boolean,
            edit: Boolean,
            del: Boolean
        }
    },
    methods: {
        toggleEditContact(contact) {
            contact.edit = !contact.edit;
        }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    * {
        box-sizing: border-box;
    }
    .contact {
        position: relative;
        border-top: 1px solid #2c3e50;
        display: inline-block;
        width: 100%;
        padding: 10px 20px;
        text-align: left;
    }
    .called {
        background-color: #353739ab;
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
</style>