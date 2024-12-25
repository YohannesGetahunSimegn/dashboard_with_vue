<template>
  <div class="app">
    <header>
      <h1>Simple Dashboard</h1>
      <p>Your can add and remove a user here!</p>
    </header>

    <main class="main-content">
      <!-- Remove User Section -->
      <div class="remove-user-container">
        <h2>Remove User</h2>
        <div>
          <input
            v-model="userIdToRemove"
            type="number"
            placeholder="Enter user ID to remove"
          />
          <Button
            @click="handleRemoveUser"
            :disabled="!userIdToRemove"
            type="danger"
          >
            Remove User
          </Button>
        </div>
      </div>

      <!-- Add User Section -->
      <div class="add-user-container">
        <h2>Add User</h2>
        <div>
          <input
            v-model="newUser.name"
            type="text"
            placeholder="Enter name"
            :disabled="addingUser"
          />
          <input
            v-model="newUser.email"
            type="email"
            placeholder="Enter email"
            :disabled="addingUser"
          />
          <Button
            @click="handleAddUser"
            :disabled="!newUser.name || !newUser.email || addingUser"
            type="primary"
          >
            Add User
          </Button>
        </div>
      </div>

      <!-- Data Table Section -->
      <div class="data-table-container">
        <h2>User Data</h2>
        <!-- <Button @click="handleAddRow" :disabled="false" type="primary">
          Add Random User
        </Button> -->
        <DataTable
          :columns="columns"
          :rows="rows"
          :pagination="true"
          :itemsPerPage="5"
        />
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { DataTable, Button } from "@swarmakit/vue";
import "@swarmakit/vue/dist/style.css"; // Import Swarmakit's global styles

// User data for the table
const columns = [
  { key: "id", label: "ID", sortable: true },
  { key: "name", label: "Name", sortable: true },
  { key: "email", label: "Email", sortable: false },
  { key: "role", label: "Role", sortable: false },
];

const rows = ref([
  { id: 1, name: "John Doe", email: "john.doe@example.com", role: "Admin" },
  { id: 2, name: "Jane Smith", email: "jane.smith@example.com", role: "User" },
]);

// User ID to remove from the table
const userIdToRemove = ref(null);

// New user data
const newUser = ref({
  name: "",
  email: "",
});

// State to track if a user is being added
const addingUser = ref(false);

// Function to add a random user to the data table
const handleAddRow = () => {
  const newRow = {
    id: rows.value.length + 1,
    name: "Random User",
    email: `user${rows.value.length + 1}@example.com`,
    role: "Guest",
  };
  rows.value.push(newRow);
};

// Function to add a user from the form
const handleAddUser = () => {
  addingUser.value = true;
  const newRow = {
    id: rows.value.length + 1,
    name: newUser.value.name,
    email: newUser.value.email,
    role: "User",
  };
  rows.value.push(newRow);
  newUser.value.name = "";
  newUser.value.email = "";
  addingUser.value = false;
};

// Function to remove a user by ID
const handleRemoveUser = () => {
  const userId = userIdToRemove.value;
  const index = rows.value.findIndex((user) => user.id === userId);
  if (index !== -1) {
    rows.value.splice(index, 1);
    userIdToRemove.value = null; // Reset input after removal
  } else {
    alert("User not found");
  }
};
</script>

<style scoped>
.app {
  font-family: Arial, sans-serif;
  padding: 20px;
  background-color: #f4f4f9;
  color: #333;
}

header {
  text-align: center;
  margin-bottom: 30px;
}

header h1 {
  font-size: 2.5rem;
}

header p {
  font-size: 1.2rem;
  color: #777;
}

.main-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.remove-user-container,
.add-user-container,
.data-table-container {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

input {
  padding: 8px;
  font-size: 1rem;
  margin-right: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
  margin-bottom: 10px;
}

button {
  font-size: 1rem;
}
</style>
