<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Email:</label>
    <input type="email" name="" id="" required v-model="email">

    <label for="">Password:</label>
    <input type="password" name="" id="" required v-model="password">
    <div class="error" v-if="passwordError"> {{ passwordError }} </div>

    <label for="">Role</label>
    <select>
        <option value="developer">Web developer</option>
        <option value="designer">Web designer</option>
    </select>

    <label>Skills:</label>
    <!-- <input type="text" v-model="tempSkill" @keyup.alt="addSkill"> -->
    <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{ skill }} </span>
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Create an Account</button>
    </div>

    <!-- <div>
        <input type="checkbox" value="Shoun" v-model="names">
        <label>Shoun</label>
    </div>
    <div>
        <input type="checkbox" value="Yoshi" v-model="names">
        <label>Yoshi</label>
    </div>
    <div>
        <input type="checkbox" value="Mario" v-model="names">
        <label>Mario</label>
    </div> -->

  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Skills: {{ skils }}</p>
  <p>Terms: {{ terms }}</p>
  <!-- <p>Names: {{ names }}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email : '',
            password: '',
            role: 'designer',
            terms: false,
            tempSkill:'',
            skills: [],
            passwordError: ''
            // names: []
        }
    },
    methods: {
        addSkill(e) {
            if(e.key === ',' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                    this.tempSkill = ''
                }
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill!== item
            })
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ?
            '' : 'Password must be at least 6 char long'

            if(!this.passwordError) {
                console.log('email',this.email);
                console.log('password',this.password);
                console.log('role',this.role);
                console.log('skills',this.skills);
                console.log('terms accepted',this.terms);
            }
        }
    }

}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
        cursor: pointer;
    }
    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
        cursor: pointer;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>