<template>
  <div id="app">
    <h1>Système de Suivi des Réclamations</h1>

    <!-- Formulaire de réclamation -->
    <form @submit.prevent="submitComplaint" class="complaint-form">
      <div class="form-group">
        <label for="title">Titre de la réclamation</label>
        <input type="text" v-model="newComplaint.title" id="title" required />
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <textarea v-model="newComplaint.description" id="description" required></textarea>
      </div>
      <div class="form-group">
        <label for="status">Statut</label>
        <select v-model="newComplaint.status" id="status" required>
          <option value="Nouvelle">Nouvelle</option>
          <option value="En cours">En cours</option>
          <option value="Résolue">Résolue</option>
        </select>
      </div>
      <button type="submit" class="add-btn">Ajouter Réclamation</button>
    </form>

    <!-- Liste des réclamations -->
    <div class="complaint-list">
      <h2>Liste des Réclamations</h2>
      <ul>
        <li v-for="complaint in complaints" :key="complaint.id" class="complaint-item">
          <h3>{{ complaint.title }}</h3>
          <p>{{ complaint.description }}</p>
          <p><strong>Statut :</strong> {{ complaint.status }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newComplaint: {
        title: "",
        description: "",
        status: "Nouvelle",
      },
      complaints: [],
    };
  },
  methods: {
    submitComplaint() {
      if (this.newComplaint.title && this.newComplaint.description) {
        const complaint = {
          id: Date.now(),
          title: this.newComplaint.title,
          description: this.newComplaint.description,
          status: this.newComplaint.status,
        };
        this.complaints.push(complaint);
        this.resetForm();
      }
    },
    resetForm() {
      this.newComplaint.title = "";
      this.newComplaint.description = "";
      this.newComplaint.status = "Nouvelle";
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
  max-width: 600px;
  margin: auto;
  font-family: Arial, sans-serif;
  color: #4a4a4a;
}

h1 {
  font-size: 2.2em;
  color: #ff6f91;
  margin-bottom: 1em;
  font-weight: 600;
}

.complaint-form {
  background-color: #ffe4e6;
  padding: 1.5em;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 2em;
  transition: transform 0.3s ease;
}

.complaint-form:hover {
  transform: scale(1.02);
}

.form-group {
  margin-bottom: 1em;
}

label {
  display: block;
  font-weight: 500;
  color: #ff6f91;
  margin-bottom: 0.5em;
}

input[type="text"],
textarea,
select {
  width: 100%;
  padding: 0.8em;
  border-radius: 4px;
  border: 1px solid #ffb3b3;
  background-color: #fff5f5;
  transition: border-color 0.3s;
}

input[type="text"]:focus,
textarea:focus,
select:focus {
  border-color: #ff6f91;
  outline: none;
}

.add-btn {
  background-color: #ff6f91;
  color: white;
  padding: 0.7em 1.2em;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1em;
  transition: background-color 0.3s ease;
}

.add-btn:hover {
  background-color: #ff8fa1;
}

.complaint-list h2 {
  color: #ff6f91;
  font-size: 1.8em;
  margin-bottom: 0.5em;
}

ul {
  list-style: none;
  padding: 0;
}

.complaint-item {
  background: #fff5f5;
  padding: 1em;
  margin: 1em 0;
  border-radius: 8px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.complaint-item:hover {
  background-color: #ffebee;
  transform: scale(1.02);
}

h3 {
  font-size: 1.5em;
  color: #d66382;
}

p {
  color: #7a7a7a;
}
</style>
