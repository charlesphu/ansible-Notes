# Yaml Basics

## Basics

- All Yaml start with `---` and end with `...`
    ```bash
    ---
    <Yaml>
    ...
    ```

- Lists start with a `-`
    ```bash
    ---
    - Apple
    - Bananna
    - Peach
    - Strawberry
    ...
    ```
    - abbreviated form: `["Apple", "Bananna", "Peach", "strawberry"]`

- Dictionaries are represented as `key:value` pair
    ```bash
    ---
    car:
        manufacturer: toyota
        miles: 88000
        engine: inline 4
        model: prius
    ...
    ```
    - abbreviated form: `car: {manufacturer: toyota, miles: 88000, engine: inline 4, model: prius}`
- you can chain lists and dictionaries together
    ```bash
    ---
    - car1:
        manufacturer: toyota
        miles: 88000
        engine: inline 4
        model: prius
    - car2:
        manufacturer: honda
        miles: 99000
        engine: inline 4
        model: civic
    ...
    ```
- for boolean values use lowercase `true` `false`


