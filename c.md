# C Style Guide

## General

- Code should use `2` spaces for indents, *not* tabs.

- Use `1` space between between keyword and opening bracket

- Operators should be spaced around:
  ```c
  int z = x * y;
  ```
  Not
  ```c
  int z=x*y;
  ```

- Code should avoid indentation levels greater than three. Favor extraction or
  inversion. Bad code would look like this:
  ```c
  for (int i = 0; i < 10; i++) {
    if (bool) {
      for (int j = 0; j < 15; j++) {
        if (array[j] == thing) {
          return true;
        } else {
          return false;
        }
      }
    } else {
      return false;
    }
  }
  ```
  Inversion can be applied to this code by prioritizing the unhappy path:
  ```c
  if (!bool) {
    return false
  }

  for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 15; j++) {
      if (array[j] != thing) { return false; }

      state.push(*array[j]);
      return true;
    }
  }
  ```
  This code might not fit your fancy, but the general indentation level is reduced.

- Opening braces should be on the same line as the start of the if statement,
  function, class, etc. following a space.
  ```c
  if (bool) {
  }

  void function() {
  }
  ```

- Else statement should be on the same line as the closing brace of it's
  corresponding if statement
  ```c
  if (bool) {
  } else {
  }
  ```

- Space padding is generally not used, but there are two exceptions.
  For one liners using brackets, space padding is preffered:
  ```c
  #define SWAP(a, b) do { a ^= b; b ^= a; a ^= b; } while (0)

  if (!bool) { return false; };
  ```
  For variable assignment using parenthesis, space padding is preffered:
  ```c
  x = ( y * 0.5f );
  ```
  Not
  ```c
  x = (y * 0.5f);
  ```

- Precision specification for floats is preferred.
  ```c
  float y = 1.5f;
  ```
  Instead of
  ```c
  float y = 1.5;
  ```
  And
  ```c
  float y = 1.0f;
  ```
  Not
  ```c
  float y = 1.f;
  ```

## Naming

- **DO NOT USE HUNGARIAN NOTATION**
  It's 20XX ffs, use an lsp you buffoon

### File Names

- Source files should have extension `.c`.

- Header files should have extension `.h`.

- File names should be `snake_case` and **NEVER** be uppercase.

### Variables

- Variables should be `snake_case`

### Functions

- Functions should be `snake_case`.

- Functions assosciated with struct's should follow format `struct_function`:
  ```c
  struct Car {
    bool on;
  }

  void car_start(struct Car *self) {
    self.on = true;
  }
  ```

- Internal struct functions and data (private if you're a new age jackass)
  should be prefixed with `_`:
  ```c
  void _renderer_setpixel(struct Renderer *self) {
    ...
  }

  void renderer_drawline(struct Renderer *self) {
    ...
    _renderer_setpixel(*self);
  }
  ```

### Structs

- Structs should be`CamelCase`.

- All struct members should be `snake_case`.

- TODO typedef?

### Enums

- Enums should be `CamelCase`.

- Enum values should be `SCREAMING_SNAKE_CASE`.

### Macros, Defines, & Constants

- Defined names and macros should be `SCREAMING_SNAKE_CASE`.

- Macros should be somewhat avoided. However, if necessary, should be
  `SCREAMING_SNAKE_CASE`, with a project-specific prefix:
  ```c
  #define PROJECT_ADD(x, y) ...
  ```

- Constants should be `SCREAMING_SNAKE_CASE`


## C Version

TODO


## Header Files

- Header files should have unique `#define` guards. These ensure that a header
  is only included once.
