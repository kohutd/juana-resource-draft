This:

```juana
name = "Users and pets database"
version = "1.0.0"

int int64;

/// users
UserData {
  name: string;
  email: string;
}

UserInput has UserData {
}

UserResult has UserData {
  id: int;
}

@resource "users" UserInput UserResult;

/// pets
PetData {
  name: string;
  userId: int;
}

PetInput has PetData {
}

PetResult has PetData {
  id: int;
}

@resource "pets" PetInput PetResult {
  getAllByUserId(userId: int): PetResult[];
}
```

Will generate:

```juana
name = "Users and pets database"
version = "1.0.0"

int int64;

/// users
UserData {
  name: string;
  email: string;
}

UserInput has UserData {
}

UserResult has UserData {
  id: int;
}

users.create(user: UserInput): UserResult;
users.update(id: int, user: UserInput): UserResult;
users.delete(id: int): void;
users.getAll(): UserResult[];
users.getPage(page: int, perPage: int): UserResult[];
users.getById(id: int): UserResult;

/// pets
PetData {
  name: string;
  userId: int;
}

PetInput has PetData {
}

PetResult has PetData {
  id: int;
}

pets.create(pet: PetInput): PetResult;
pets.update(id: int, pet: PetInput): PetResult;
pets.delete(id: int): void;
pets.getAll(): PetResult[];
pets.getAllByUserId(userId: int): PetResult[];
pets.getPage(page: int, perPage: int): PetResult[];
pets.getById(id: int): PetResult;
```
