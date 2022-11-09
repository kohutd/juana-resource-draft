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

@resource "users" "int" UserInput UserResult;

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

@resource "pets" "int" PetInput PetResult {
  getAllByUserId(userId: int): PetResult[];
}
```

Will be transformed to this:

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
users.updateById(id: int, user: UserInput): UserResult;
users.deleteById(id: int): void;
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
pets.updateById(id: int, pet: PetInput): PetResult;
pets.deleteById(id: int): void;
pets.getAll(): PetResult[];
pets.getPage(page: int, perPage: int): PetResult[];
pets.getById(id: int): PetResult;
pets.getAllByUserId(userId: int): PetResult[];
```
