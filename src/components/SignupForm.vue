<template>
  <form @submit.prevent="handleSubmit">
    <label>Email: </label>
    <input type="email" required v-model="email" />

    <label>Passowrd: </label>
    <input type="password" required v-model="password" />

    <label>Role: </label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <div class="skills">
      <label for="">Skills</label>
      <input type="text" v-model="tempSkill" @keyup="addSkill" />
      <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
      </div>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button type="submit">Create an account</button>
    </div>
  </form>

  <p>email: {{ email }}</p>
  <p>passowrd: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      tempSkill: "",
      skills: [],
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill.trim().slice(0, -1))) {
          this.skills.push(this.tempSkill.trim().slice(0, -1));
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills.splice(this.skills.indexOf(skill), 1);
    },
    handleSubmit() {
      console.log({
        email: this.email,
        password: this.password,
        role: this.role,
        terms: this.terms,
        skills: this.skills,
      });
    },
  },
};
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
input,
select {
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
  color: #fff;
  border-radius: 20px;
}
button:hover {
  background: #0b6dffcc;
  cursor: pointer;
}
.submit {
  text-align: center;
}
</style>