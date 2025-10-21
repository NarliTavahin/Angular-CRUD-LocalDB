# Angular CRUD with LocalDB

This repository demonstrates a full CRUD (Create, Read, Update, Delete) application built using **Angular** and **LocalDB** for data persistence. The app allows users to perform basic operations (create, read, update, and delete entries) locally, without relying on external APIs. LocalDB ensures that data is stored on the user's device, making it ideal for applications where you need offline functionality.

## Features
- **Create**: Add a new item to the local database.
- **Read**: Fetch and display a list of items from LocalDB.
- **Update**: Modify an existing item's information in LocalDB.
- **Delete**: Remove an item from LocalDB.
- **LocalDB Integration**: All data is stored locally in the browser, making the application offline-capable.
- **Responsive UI**: Built with Angular and responsive CSS to work on desktop and mobile.

## Installation

### Prerequisites
- Node.js (>=12.0.0)
- Angular CLI (>=12.0.0)
- **json-server** for local API (optional)

### Steps to Get Started

1. **Clone the repository**:
   ```bash
   git clone https://github.com/NarliTavahin/Angular-CRUD-LocalDB.git
   cd Angular-CRUD-LocalDB
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Install json-server globally** (optional, if you want to simulate an API):
   ```bash
   npm install -g json-server
   ```

4. **Run the application**:
   ```bash
   ng serve
   ```

   The application will be running at `http://localhost:4200/`.

5. **Start json-server** (optional):
   - To simulate a backend API, create a `db.json` file and start the JSON server:
   ```bash
   json-server --watch db.json --port 3000
   ```
   This will start a fake API on `http://localhost:3000/` that can be used for local data management.


- **User Create**:
    ![User Create](https://github.com/NarliTavahin/Angular-CRUD-LocalDB/blob/main/photos-videos/Create.png)

- **User Read**:
    ![User Read](https://github.com/NarliTavahin/Angular-CRUD-LocalDB/blob/main/photos-videos/Read.png)

- **User Update**:
    ![User  Update](https://github.com/NarliTavahin/Angular-CRUD-LocalDB/blob/main/photos-videos/Update.png)
  
- **User Delete**:
    ![User Delete](https://github.com/NarliTavahin/Angular-CRUD-LocalDB/blob/main/photos-videos/Delete.png)

- **User Login****:
    ![User Login](https://github.com/NarliTavahin/Angular-CRUD-LocalDB/blob/main/photos-videos/Login.png)

- **User List**:
    ![User List](https://github.com/NarliTavahin/Angular-CRUD-LocalDB/blob/main/photos-videos/List.png)


## Technologies Used

- **Angular**: Frontend framework
- **LocalDB**: Local storage solution for browser-based data persistence
- **RxJS**: For managing asynchronous data streams
- **Bootstrap**: For responsive UI styling (Optional: If you are using Bootstrap)
- **json-server**: For creating a fake API to simulate backend requests (Optional)

## LocalDB Implementation

LocalDB is used in this application to store and retrieve data directly from the user's browser. 
It offers an easy solution for applications that require offline functionality without needing an external server.

### Example of Using LocalDB:

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LocalStorageService {

  private localDB: any = window.localStorage;

  constructor() {}

  // Add a new user to LocalDB
  addUser(user: any): void {
    const users = JSON.parse(this.localDB.getItem('users') || '[]');
    users.push(user);
    this.localDB.setItem('users', JSON.stringify(users));
  }

  // Get all users from LocalDB
  getUsers(): any[] {
    return JSON.parse(this.localDB.getItem('users') || '[]');
  }

  // Update a user in LocalDB
  updateUser(updatedUser: any): void {
    const users = this.getUsers();
    const userIndex = users.findIndex((user: any) => user.id === updatedUser.id);
    if (userIndex !== -1) {
      users[userIndex] = updatedUser;
      this.localDB.setItem('users', JSON.stringify(users));
    }
  }

  // Delete a user from LocalDB
  deleteUser(userId: number): void {
    let users = this.getUsers();
    users = users.filter((user: any) => user.id !== userId);
    this.localDB.setItem('users', JSON.stringify(users));
  }
}
```


## Acknowledgements

- [Angular](https://angular.io/) for the powerful framework.
- [LocalDB](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) for local data persistence.
- [Bootstrap](https://getbootstrap.com/) for the responsive design.
- [json-server](https://github.com/typicode/json-server) for creating a fake backend.

---

Feel free to open issues for bugs or improvements. Happy coding! 🚀
