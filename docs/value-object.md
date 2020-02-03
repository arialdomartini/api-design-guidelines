Value Object
============
Differently from an Entity, a Value Object is an immutable type that is distinguishable only by the state of its properties. As such, it has no identity, and no URI to represent itself.

As an example, consider the entity User:

```json
{
    "name": string,
    "age": int,
    "avatar": image
}
```

and 2 user entities whose URIs are

```
/users/9b16b870-5074-49b1-8f04-e119e7a692fb
/users/12dafd83-3ded-41aa-ab74-6a6ba4592b38
```

They are distinguished (i.e. they have different identies) no matter their states, that is, even if all the values of their fields are the same.

On the contrary, when their fields `name` have the same value "John", the 2 strings "John" are indistinguishable. They have no identity, and they are in fact the same.


