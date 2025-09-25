These are **Spring stereotypes annotations** that tell the container *what role a class plays* in the application. Let’s go one by one:

---

## 🔹 `@RestController`

* A **specialized controller** in Spring MVC.
* Combines `@Controller` + `@ResponseBody`.
* Used for **RESTful APIs** where you return **JSON/XML** instead of HTML views.
* Methods inside usually return **objects** → automatically converted (serialized) into JSON by Jackson.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    
    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.getUserById(id); // returns JSON
    }
}
```

---

## 🔹 `@Service`

* Marks a class as a **Service Layer** component.
* Typically contains **business logic**.
* Tells Spring to create a **singleton bean** of this class and inject it where needed.

```java
@Service
public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User getUserById(Long id) {
        return userRepository.findById(id)
                             .orElseThrow(() -> new RuntimeException("User not found"));
    }
}
```

---

## 🔹 `@Repository`

* Marks a class as a **DAO (Data Access Layer)**.
* Usually interacts with **databases**.
* Benefits:

  * Makes the class a **Spring bean**.
  * Translates database exceptions into **Spring’s DataAccessException** (a unified unchecked exception).

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    // Spring Data JPA auto-implements methods
}
```

---

## 🔹 `@Component`

* **Generic stereotype annotation**.
* Marks a class as a Spring-managed bean, without specifying its role (Controller, Service, Repository).
* Used when the class doesn’t clearly fall into the above categories.

```java
@Component
public class EmailValidator {
    public boolean isValid(String email) {
        return email.contains("@");
    }
}
```

---

## ✅ Summary Table

| Annotation        | Layer / Purpose                | Extra Behavior                              |
| ----------------- | ------------------------------ | ------------------------------------------- |
| `@RestController` | Controller layer (REST APIs)   | Combines `@Controller` + `@ResponseBody`    |
| `@Service`        | Service layer (Business logic) | Clearer semantics, business rules live here |
| `@Repository`     | Data access layer (DB ops)     | Exception translation                       |
| `@Component`      | Generic Spring bean            | No extra behavior, just a managed bean      |

---

👉 Quick Interview Tip:
If asked *“Difference between `@Component`, `@Service`, `@Repository`?”* — say:

> *“They all make a class a Spring bean, but `@Service` and `@Repository` add semantic meaning and enable additional features, like exception translation in `@Repository`. They help make the code more readable and layered.”*

---

Do you want me to also explain **the flow** (how `@RestController` calls `@Service`, which calls `@Repository`), since that’s often asked in interviews?
