# task-7
Use JavaScript Fetch API to get user data from:
https://jsonplaceholder.typicode.com/users

Display user name, email, and address.

Handle loading and error states.

Add a reload button.

Style it with CSS.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>User Data Fetcher</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f9f9f9;
      padding: 30px;
      text-align: center;
    }

    h1 {
      color: #333;
    }

    #userList {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin-top: 20px;
      gap: 20px;
    }

    .user-card {
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      padding: 15px 20px;
      width: 250px;
      text-align: left;
    }

    .user-card h3 {
      margin-top: 0;
    }

    .error {
      color: red;
      font-weight: bold;
    }

    #reloadBtn {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }

    #reloadBtn:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>

  <h1>📦 Fetch Users from Public API</h1>
  <div id="userList">Loading users...</div>
  <button id="reloadBtn">🔄 Reload Users</button>

  <script>
    const userList = document.getElementById("userList");
    const reloadBtn = document.getElementById("reloadBtn");

    async function fetchUsers() {
      userList.innerHTML = "Loading users...";
      try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");

        if (!response.ok) {
          throw new Error("Failed to fetch data: " + response.status);
        }

        const users = await response.json();
        userList.innerHTML = "";

        users.forEach(user => {
          const card = document.createElement("div");
          card.className = "user-card";
          card.innerHTML = `
            <h3>${user.name}</h3>
            <p><strong>Email:</strong> ${user.email}</p>
            <p><strong>Address:</strong> ${user.address.street}, ${user.address.city}</p>
          `;
          userList.appendChild(card);
        });

      } catch (error) {
        userList.innerHTML = `<p class="error">⚠️ ${error.message}</p>`;
      }
    }

    // Load users on page load
    fetchUsers();

    // Reload button functionality
    reloadBtn.addEventListener("click", fetchUsers);
  </script>

</body>
</html>
