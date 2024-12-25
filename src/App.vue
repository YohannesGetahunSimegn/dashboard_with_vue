<template>
  <div class="app">
    <header>
      <h1>Simple Dashboard</h1>
      <p>Welcome to your dashboard! Here's a quick overview of your data.</p>
    </header>

    <main class="main-content">
      <div class="calendar-container">
        <h2>Upcoming Events</h2>
        <CalendarView :events="events" />
      </div>

      <div class="data-table-container">
        <h2>User Data</h2>
        <!-- Updated DataTable with proper props -->
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
import { CalendarView, DataTable } from "@swarmakit/vue";

const events = [
  { date: "2024-12-25", title: "Christmas Celebration" },
  { date: "2024-12-31", title: "New Year's Eve Party" },
];

// DataTable props
const columns = [
  { key: "id", label: "ID", sortable: true },
  { key: "name", label: "Name", sortable: true },
  { key: "email", label: "Email", sortable: false },
  { key: "role", label: "Role", sortable: false },
];

const rows = [
  { id: 1, name: "John Doe", email: "john.doe@example.com", role: "Admin" },
  { id: 2, name: "Jane Smith", email: "jane.smith@example.com", role: "User" },
  {
    id: 3,
    name: "Alice Johnson",
    email: "alice.johnson@example.com",
    role: "Moderator",
  },
];

const handleActionClick = () => {
  alert("Action performed!");
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
  margin-bottom: 30px;
}

.main-content > div {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h2 {
  font-size: 1.6rem;
  margin-bottom: 15px;
}

footer {
  text-align: center;
  margin-top: 30px;
}

footer .swarm-button {
  background-color: #4caf50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

footer .swarm-button:hover {
  background-color: #45a049;
}
</style>
