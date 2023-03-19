```typescript
/**
 * 1 - Intersection Types: An intersection type allows you to combine multiple types into one.
 */
interface Person2 {
  name: string
  age: number
}

interface Employee {
  jobTitle: string
  salary: number
}

type PersonAndEmployee = Person2 & Employee

const person: PersonAndEmployee = {
  name: 'John',
  age: 30,
  jobTitle: 'Software Engineer',
  salary: 100000,
}


/**
 * 2 - Union types: 
 
 
 
 amples
 */
type Gender = 'male' | 'female'
type Direction = 'up' | 'down' | 'left' | 'right'

const gender: Gender = 'male'
const direction: Direction = 'up'

const myVar: (string | number)[] = ['hello', 42, 'world', 99]


/**
 * 3 - Type Guards: Type guards are used to narrow down the type of a variable within a conditional statement.
 */
type Person1 = { name: string } | { age: number }

function greet(person: Person1) {
  if ('name' in person) {
    console.log(`Hello, ${person.name}!`)
  } else {
    console.log(`You are ${person.age} years old.`)
  }
}

greet({ name: 'John' }) // logs 'Hello, John!'
greet({ age: 30 }) // logs 'You are 30 years old.'


/**
 * 4 - Conditional Types: Conditional types allow you to conditionally map one type to another based on a condition.
 */
type IsString<T> = T extends string ? true : false

type A = IsString<string> // true
type B = IsString<number> // false


/**
 * 4.1 - Conditional Types
 */
type Room = {
  name: string
  area: number
}

type Garage = {
  size: number
}

// example - 1 [intersection]
type House<T extends Room, HasGarage extends boolean> = {
  address: string
  rooms: T[]
} & (HasGarage extends true ? { garage: Garage } : {})

const houseExample1: House<Room, true> = {
  address: '',
  rooms: [
    {
      area: 1,
      name: ''
    }
  ],
  garage: {
    size: 1
  }
}

// example - 2 [conditional with union type]
type House2<T extends Room> = {
  address: string
  rooms: T[]
  hasGarage: true
  garage: Garage
} | {
  address: string
  rooms: T[]
  hasGarage: false
}

const houseExample2: House2<Room> = {
  address: '',
  rooms: [
    {
      area: 1,
      name: ''
    }
  ],
  hasGarage: true,
  garage: {
    size: 1
  }
}


/**
 * 5 - Mapped Types: Mapped types allow you to create a new type by iterating over the properties of an existing type.
 */
interface Person2 {
  name: string
  age: number
}

type ReadonlyPerson<T> = {
  readonly [P in keyof T]: T[P]
}

const person2: Person2 = { name: 'John', age: 30 }
const readonlyPerson: ReadonlyPerson<Person2> = Object.freeze(person2)

// readonlyPerson.age = 31 // error: Cannot assign to 'age' because it is a read-only property.

/**
 * 5.1 - Mapped Types 
 * T[keyof T] returns the type of the value at each of those keys.
 */
type ValueOf<T> = T[keyof T]

type VideoGame = {
  name: 'playstation',
  value: '2500'
}

const videoGameValue: ValueOf<VideoGame> = '2500'
const videoGameName: ValueOf<VideoGame> = 'playstation'


/**
 * 6 - Ensure that a particular value is of a specific subtype of a larger type using a custom type(PickUnionType) or extends
 */
type PickUnionType<T, K extends T> = K

type Objects = 'door' | 'plate' | 'bed'

// example - 1 [PickUnionType]
type PersonWithObject<T> = {
  name: string
  age: number
  object: T
}

const object: PersonWithObject<PickUnionType<Objects, 'bed'>> = {
  age: 100,
  name: 'John',
  object: 'bed'
}

// example - 2 [extends]
type PersonWithObject2<T extends Objects> = {
  name: string
  age: number
  object: T
}

const object2: PersonWithObject2<'bed'> = {
  age: 100,
  name: 'John',
  object: 'bed'
}

/**
 * 7 - Mapped and Conditional types
 */
type Teste<T> = {
  where?: {
    [K in keyof T]: {
      value: T[K],
      conditional?: 'equals' | 'different'
    } | {
      value: Array<T[K]>
      conditional?: 'in'
    }
  }
}

const teste: Teste<{ name: 'naming' }> = {
  where: {
    name: {
      value: ['naming'],
      conditional: 'in'
    }
  }
}

const teste2: Teste<{ name: 'Jack Blade' }> = {
  where: {
    name: {
      value: 'Jack Blade',
      conditional: 'different'
    }
  }
}
```
