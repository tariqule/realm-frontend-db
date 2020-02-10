# [Realm-FrontEnd-Database ](https://realm.io/products/realm-database)

![realm.io](https://raw.githubusercontent.com/realm/realm-js/master/logo.png)

## Introduction on Realm for React-Native ##

**First make schema and make current user null**

```
const currentUser = null;
  const UserSchema = { name: "User", primaryKey: "id", properties: {
id: "string",
uid: { type: "string", optional: true },
username: { type: "string", optional: true, default: "username" }, fullName: { type: "string", optional: true, default: "fullname" }, email: "string",
birthdate: { type: "date", optional: true },
photo: { type: "string", optional: true }
} };
```

**Add the Schema**
 
 ```
 export const realm = new Realm({ path: "RNChat.realm",
schema: [
UserSchema, ContactSchema, MessageSchema, MessageQueueSchema, ChatSchema
] });
```
**Add User**

```
export const addUser = user => { currentUser = user; realm.write(() => {
realm.create("User", { id: uuid.v1(),
 
 uid: user.uid, email: user.email, username: user.email
}); });
};
```

**Update user**

```
export const updateUser = ({ fullName, username }) => { realm.write(() => {
realm.create( "User",
{
id: currentUser.id, username: username, fullName: fullName
},
true
); });
};
```

**Delete User**
 
 ```
export const deleteAll = () => { realm.write(() => {
let users = realm.objects("User"); realm.delete(users);
}); };
```
 
**Get Current user**

```
  export const getCurrentUser = () => { let users = realm.objects("User"); if (users.length > 0) {
users.forEach(user => { currentUser = user;
}); }
return currentUser; };
```

## Authors

* **Tariqule Khan** - *Initial work* - [MyBee](https://github.com/mybeeapp)
