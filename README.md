# Awesome inspiring quote first

>  Clean code is simple and direct. Clean code reads like well-written
> prose. Clean code never obscures the designer’s intent but rather is
> full of crisp abstractions and straightforward lines of control.
>   
> Grady Booch

and now for the rules I tend to use in my everyday practice
# Naming

## Any name should reflect intention

Bad:
```
function addToDate(date, month) {
    // ...
}

const date = new Date();
addToDate(date, 1); // huh, what are we adding?
```
Good:
```
function addMonthToDate(date, month) {
    // ...
}

const date = new Date();
addMonthToDate(date, 1);
```

## Code should be understandable without meaningless comments (mumbling)

Bad:

```
// Get filtered list of hosts from DB
await getHosts(f);
```

Good:
```
await getHostsFromDB(filterCondition);
```

## Don't use meaningless suffixes (Manager/Controller/Helper etc.)

Bad:
```
class FeedManager { /* ... */ }

class UserService { /* ... */ }
```

Good:
```
class FeedUpdateScheduler { /* ... */ }

class UserHttpApi { /* ... */ }
```

## The larger the scope, the more verbose names

Bad:
```
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l);
});
```

Good:
```
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => doStuff(l));
```

# Single Responsibility Principle
Ideally every method, class or just any abstraction should only do one thing. So the only reason to change the abstraction is the change of requirements. I don't beleive in Open-Closed Principle cause it overcomplicates thing, but follow the idea that we shouldn't mix levels of abstractions:
* _low level_
  - working with files
  - http requests
  - database queries
  - MQ events
* middle level
  - Normalization
  - Data transformation
  - Formatting
* High level
    - Application business logic.

Bad:

[Codesample of doom](https://www.youtube.com/watch?v=ODQ0SesuGwI)

Good:
```
class ActiveDirectoryIntegration {
  /* ... */
  async run() {
    await this.ensureDomainExists();
    await this.updateStaff();
    await this.updateStaffPirvilleges();
    await this.sendChangeLog();
  }
}
```

# Avoid premature abstractions
* Developer1 sees the code duplication, makes an abstraction, feels good about himself — he follows DRY
* Developer2 sees the abstraction that doesn't fit his needs but decides it's there's a reason for this abstraction to exist. He adds an if/else condition
* Developer3 does the same
* ...
* You're now here and life is shit.

# Work in short iteractions to keep focus
* Rewriting something from scratch is not a refactoring
* Commit often
* Hell yeah, TDD


(extracted from my talk in russian: https://www.youtube.com/watch?v=R4-uveKppV8)
