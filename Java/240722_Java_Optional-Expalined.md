# Optional Explained

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/23
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

When using JPA and hibernate as ORM frameworks, the `Optional<T>` type is frequently used in the repositories. Furthermore, the `Optional<T>` has its own methods which proceeds the null check, filtering, and excpetion throwing with chaining. The reason why `Optional<T>` is preferred could be found in the various features.

### Tackling Curiosity

**Optional.html**

The `Optional<T>` class was introduced at `Java 1.8`. The oracle docs describes the `Optional<T>` class like below. Let's start with the descriptions from the oracle docs.

> A container object which may or may not contain a non-null value. If a value is present, isPresent() will return true and get() will return the value.
> Additional methods that depend on the presence or absence of a contained value are provided, such as orElse() (return a default value if value not present) and ifPresent() (execute a block of code if the value is present).
> This is a value-based class; use of identity-sensitive operations (including reference equality (==), identity hash code, or synchronization) on instances of Optional may have unpredictable results and should be avoided.
