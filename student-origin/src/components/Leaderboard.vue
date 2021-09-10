<template>
  <div class="Container">
    <h1 class="mt-4 text-center">Student Origin</h1>
    <form action="">
      <div class="form-group">
        <label for="state">Select State of Origin</label>
        <select v-model="state" class="form-control" name="state" id="states">
          <option value="Abia">Abia</option>
          <option value="Adamawa">Adamawa</option>
          <option value="Akwa Ibom">Akwa Ibom</option>
          <option value="Anambra">Anambra</option>
          <option value="Bauchi">Bauchi</option>
          <option value="Bayelsa">Bayelsa</option>
          <option value="Benue">Benue</option>
          <option value="Borno">Borno</option>
          <option value="Cross River">Cross River</option>
          <option value="Delta">Delta</option>
          <option value="Ebonyi">Ebonyi</option>
          <option value="Edo">Edo</option>
          <option value="Ekiti">Ekiti</option>
          <option value="Enugu">Enugu</option>
          <option value="Gombe">Gombe</option>
          <option value="Imo">Imo</option>
          <option value="Jigawa">Jigawa</option>
          <option value="Kaduna">Kaduna</option>
          <option value="Kano">Kano</option>
          <option value="Katsina">Katsina</option>
          <option value="Kebbi">Kebbi</option>
          <option value="Kogi">Kogi</option>
          <option value="Kwara">Kwara</option>
          <option value="Lagos">Lagos</option>
          <option value="abuja">Federal Capital Territory</option>
          <option value="Nasarawa">Nasarawa</option>
          <option value="Niger">Niger</option>
          <option value="Ogun">Ogun</option>
          <option value="Ondo">Ondo</option>
          <option value="Osun">Osun</option>
          <option value="Oyo">Oyo</option>
          <option value="Plateau">Plateau</option>
          <option value="Rivers">Rivers</option>
          <option value="Sokoto">Sokoto</option>
          <option value="Taraba">Taraba</option>
          <option value="Yobe">Yobe</option>
          <option value="Zamfara">Zamfara</option>
        </select>
        <label for="name">Full name</label>
        <input
          type="text"
          name="name"
          id="student"
          class="form-control"
          v-model="name"
        />
      </div>
      <button type="button" @click="onSubmit" class="btn btn-dark">
        Submit
      </button>
    </form>
    <table class="table mt-5">
      <thead>
        <tr>
          <th scope="col">Index</th>
          <th scope="col">State Of Origin</th>
          <th scope="col">Student Name</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(entry, i) in sortedList" :key="i">
          <td scope="row">{{ ++i }}</td>
          <td>{{ entry.state }}</td>
          <td>{{ entry.name }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'Leaderboard',
  data: () => ({ name: ' ', state: ' ', allStates: [] }),
  computed: {
    sortedList: function () {
      return this.allStates.slice().sort(function (a, b) {
        return b.state - a.state
      })
    },
  },
  methods: {
    onSubmit() {
      this.allStates.push({ name: this.name, state: this.state })
      this.clearForm()
    },
  },
  clearForm() {
    this.name = ' '
    this.state = ' '
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
