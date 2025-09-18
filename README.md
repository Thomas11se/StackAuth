
---

# StacksAuth -  Decentralized Social Login Contract

A smart contract built on the **Stacks blockchain** using Clarity language to provide decentralized, username-based social login functionality. It enables user registration, profile management, and account deletion in a censorship-resistant, self-sovereign manner.

---

## ⚙️ Features

* **User Registration**

  * Enforces unique usernames and validates input formats.
  * Stores `username`, `email`, and optional `profile-image` (as a URL).

* **Profile Management**

  * Update username and email.
  * Set or clear profile image.
  * Delete account and free up username.

* **Data Validation**

  * Enforces length and format constraints for usernames and emails.
  * Checks username availability before registration or update.

* **Transparency**

  * Read-only access to user data.
  * Count of total registered users.
  * Check if a principal is registered.

---

## 🛡️ Validation Rules

| Field           | Requirements                                      |
| --------------- | ------------------------------------------------- |
| `username`      | ASCII, 3–50 characters                            |
| `email`         | ASCII, 5–100 characters, must contain `@` and `.` |
| `profile-image` | Optional UTF-8 URL string, max 256 chars          |

---

## 🧠 Data Structures

### Maps

* `users: principal → { username, email, profile-image? }`
  Stores individual user data.

* `taken-usernames: string-ascii(50) → bool`
  Ensures usernames are unique across all users.

### Variables

* `user-count: uint`
  Tracks the total number of registered users.

---

## 🧩 Functions

### 📥 Public Functions

| Function                                  | Description                                                 |
| ----------------------------------------- | ----------------------------------------------------------- |
| `register-user(username, email)`          | Registers a new user with unique username and valid email.  |
| `update-profile(new-username, new-email)` | Updates current user's username/email, ensuring uniqueness. |
| `set-profile-image(image-url)`            | Sets or updates a profile image URL.                        |
| `clear-profile-image()`                   | Clears current profile image.                               |
| `delete-profile()`                        | Deletes user data and frees up the username.                |

### 🔍 Read-only Functions

| Function                          | Description                                          |
| --------------------------------- | ---------------------------------------------------- |
| `get-user-info(principal)`        | Returns user data (if exists) for a given principal. |
| `get-user-count()`                | Returns the total number of users.                   |
| `is-user-registered(principal)`   | Returns true if user is registered.                  |
| `is-username-available(username)` | Returns true if username is available for use.       |

---

## ❌ Error Messages

| Error                   | Message                                                |
| ----------------------- | ------------------------------------------------------ |
| `ERR-USER-EXISTS`       | User already exists                                    |
| `ERR-USER-NOT-FOUND`    | User not found                                         |
| `ERR-INVALID-USERNAME`  | Username must be 3–50 characters                       |
| `ERR-INVALID-EMAIL`     | Email must be 5–100 characters and contain `@` and `.` |
| `ERR-INVALID-IMAGE-URL` | Profile image must be a valid URL string               |
| `ERR-USERNAME-TAKEN`    | Username already taken                                 |

---

## 🚀 How to Use

### Registering a New User

```clarity
(register-user "satoshi" "satoshi@example.com")
```

### Updating Profile

```clarity
(update-profile "newname" "newemail@example.com")
```

### Setting a Profile Image

```clarity
(set-profile-image "https://example.com/avatar.png")
```

### Checking Username Availability

```clarity
(is-username-available "satoshi")
```

---

## ✅ Requirements

* Stacks 2.1+
* Clarity Language Support

---

## 📂 Contract Organization

```plaintext
├── Constants         ; Error messages
├── Data Maps         ; Users and usernames
├── Private Functions ; Validation helpers
├── Public Functions  ; Registration, update, delete, image handling
├── Read-only         ; Info retrieval, availability checks
```

---

## 📜 License

MIT License

---