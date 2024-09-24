<template>
    <form @submit.prevent="submit">
        <label>Email</label>
        <input type="email" v-model="email">

        <label>Password</label>
        <input type="password" v-model="password">
        <div v-if="passError" class="error">{{passError}}</div>

        <label>Rloe</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills</label>
        <input type="text" v-model="skill" @keyup="addSkill">
        <div v-for="skill in skills" :key="skill" class="skill-show">
            <span @click="delet(skill)">
                {{skill}}
            </span>
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required id="terms">
            <label for="terms">Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Sign UP</button>
        </div>
    </form>
</template>

<script>
    export default {
        data() {
            return{
                email: '',
                password: '',
                role: '',
                skill: '',
                skills: [],
                terms: false,
                names: [],
                passError: ''
            }
        },
        methods:{
            addSkill(e) {
                //add skill to skills array
                if(e.key === "Enter" && this.skill) {
                    if (!this.skills.includes(this.skill)){
                        this.skills.push(this.skill);
                    }
                    this.skill = '';
                }
            },
            delet(skill) {
                //delete skill item when click
                this.skills = this.skills.filter((item) => {
                    return skill !== item;
                })
            },
            submit() {
                let arr = [this.email,this.password,this.role,this.skills,this.terms]
                let arrStr = ["Email: ","Password: ","Role:","Skills: ","Terms: "]
                //validate pass
                this.passError = this.password.length > 5 ? console.log('submitted done') : "password must be at lest 6-chars";
                if(!this.passError) {
                    arr.forEach((ele,index) => {
                        console.log(arrStr[index], ele)
                    });
                }
            }
        }
    }
</script>

<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color:#aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
        cursor: pointer;
    }
    .skill-show{
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
    .submit{
        text-align: center;
    }
    button{
        background: #0b6dff;
        border:0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
        cursor: pointer;
    }
    .error{
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>