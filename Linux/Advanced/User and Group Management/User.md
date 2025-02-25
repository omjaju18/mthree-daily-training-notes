# Linux User and Group Management Commands 

## 1. **useradd** (Add New User)
### **Definition:**
Creates a new user account.

### **Syntax:**
```bash
useradd [options] username
```

### **Example:**
```bash
useradd omjaju
```
Creates a new user named `omjaju`.

---

## 2. **passwd** (Set/Change User Password)
### **Definition:**
Sets or changes the password for a user.

### **Syntax:**
```bash
passwd [username]
```

### **Example:**
```bash
passwd omjaju
```
Prompts to set a new password for the user `omjaju`.

---

## 3. **usermod** (Modify User Account)
### **Definition:**
Modifies an existing user account.

### **Syntax:**
```bash
usermod [options] username
```

### **Example:**
```bash
usermod -aG sudo omjaju
```
Adds `omjaju` to the `sudo` group.

---

## 4. **userdel** (Delete User Account)
### **Definition:**
Deletes a user account.

### **Syntax:**
```bash
userdel [options] username
```

### **Example:**
```bash
userdel -r omjaju
```
Deletes the user `omjaju` and their home directory.

---

## 5. **groupadd** (Create New Group)
### **Definition:**
Creates a new user group.

### **Syntax:**
```bash
groupadd groupname
```

### **Example:**
```bash
groupadd developers
```
Creates a new group named `developers`.

---

## 6. **groupdel** (Delete Group)
### **Definition:**
Deletes a user group.

### **Syntax:**
```bash
groupdel groupname
```

### **Example:**
```bash
groupdel developers
```
Deletes the `developers` group.

---

## 7. **gpasswd** (Manage Group Membership)
### **Definition:**
Adds or removes users from a group.

### **Syntax:**
```bash
gpasswd -a username groupname
```

### **Example:**
```bash
gpasswd -a omjaju developers
```
Adds `omjaju` to the `developers` group.

---

## 8. **id** (Show User ID and Group ID)
### **Definition:**
Displays user ID (UID) and group ID (GID) information.

### **Syntax:**
```bash
id [username]
```

### **Example:**
```bash
id omjaju
```
Displays the UID, GID, and group memberships of `omjaju`.

---

## 9. **who** (Show Logged-in Users)
### **Definition:**
Lists users currently logged into the system.

### **Syntax:**
```bash
who
```

### **Example:**
```bash
who
```
Displays currently logged-in users.

---

## 10. **w** (Show Active Users and Processes)
### **Definition:**
Displays logged-in users and their running processes.

### **Syntax:**
```bash
w
```

### **Example:**
```bash
w
```
Shows logged-in users and their activities.

---

## 11. **whoami** (Show Current User)
### **Definition:**
Displays the currently logged-in username.

### **Syntax:**
```bash
whoami
```

### **Example:**
```bash
whoami
```
Outputs the current user’s username.

---

## 12. **groups** (Show User Groups)
### **Definition:**
Displays the groups a user belongs to.

### **Syntax:**
```bash
groups [username]
```

### **Example:**
```bash
groups omjaju
```
Displays groups associated with `omjaju`.

---

## 13. **chown** (Change File Ownership)
### **Definition:**
Changes the owner of a file or directory.

### **Syntax:**
```bash
chown [options] user:group filename
```

### **Example:**
```bash
chown omjaju:developers file.txt
```
Changes the owner of `file.txt` to `omjaju` and the group to `developers`.

---

## 14. **chmod** (Change File Permissions)
### **Definition:**
Changes file permissions.

### **Syntax:**
```bash
chmod [permissions] filename
```

### **Example:**
```bash
chmod 755 script.sh
```
Grants read, write, and execute permissions to the owner, and read and execute permissions to others.

---

## 15. **chgrp** (Change Group Ownership)
### **Definition:**
Changes the group ownership of a file or directory.

### **Syntax:**
```bash
chgrp [group] filename
```

### **Example:**
```bash
chgrp developers file.txt
```
Changes the group ownership of `file.txt` to `developers`.

---

## Conclusion
These commands help in managing users and groups effectively in Linux. Understanding them is crucial for system administration and security.

For detailed information, use the `man` command:
```bash
man [command]
```
