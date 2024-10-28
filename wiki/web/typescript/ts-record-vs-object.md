# Typescript Record vs Object

[◀ Back](../index.md)


## Resources

[Type lvl typescript](https://type-level-typescript.com/objects-and-records) - record and object difference



### Object Types specific


```typescript
type Point = {
  x: number;
  y: number;
};

const point: Point = { x: 1, y: 2 };

const point2: Point = { x: 1, y: 2, z: 3 }; // Error: Object literal may only specify known properties, and 'z' does not exist in type 'Point'.

const point3 = { x: 1, y: 2, z: 3 };

const point4: Point = point3; // OK
```

The definitive answer is that objects with more properties are assignable to objects with fewer properties, 
but in contexts where objects are defined inline, 
TypeScript has extra rules to make sure we don't mistakenly assign props 
that we couldn't use afterward because our types would forbid us to do so.


This means that you have absolutely no guarantee that an object of some type
does not contain extra props!1 An object type is the set of objects with at least all properties it defines.

```typescript
type User = { name: string; age: number; isAdmin: boolean };

type NameOrAge = User["name" | "age"]; // => string | number
```

Which is equal to:

```typescript
type NameOrAge = User["name"] | User["age"]; // => string | number
```

Just like Object types, Records also represent sets of objects. The difference is that all keys of a record must share the same type.

```typescript
type Point = Record<"x" | "y", number>; // with is difened as follow: type Record<K, V> = { [Key in K]: V };
```

or just

```typescript

type Point = { [key: "x" | "y"], number };

const point: Point = { x: 1, y: 2 };

```

Footnotes:

1. This is why Object.keys(...) returns a string[] and
not a (keyof Obj)[] by the way. 
(keyof Obj)[] would be incorrect because Object.keys(...) 
could return strings that are not assignable to keyof Obj


2. Using too many intersection types can be detrimental to type-checking performance.
Instead of actually merging object types into one single entity, 
they keep each individual object type in memory in a sort of internal 
list of intersected types. Because of this, the type-checker needs to allocate more memory 
and will take more time to check if object types are assignable because it will need to traverse this internal list to check each object type one by one.
