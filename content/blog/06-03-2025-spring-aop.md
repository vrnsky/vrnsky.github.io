---
title: Spring AOP - Understanding proxy mechanics
type: blog
sidebar:
  open: true
date: 2025-03-06
comments: true
draft: false
---

![Under Hood](/images/2025-03-06-aop/underhood.png "Under hood")

When I first encountered Spring AOP (Aspect - Oriented Programming), it seemed like magic. My Java code began executing
extra behavior without my explicit command. Log statements showed up, transaction handled themselves, and security
check happened automatically. But as with any advanced technology, the magic has a clear explanation.

In this article, we will pull back the curtain on Spring AOP and explore how it uses proxy patterns to weave
behavior into your applications. We will look at both the theory and practical implementations so you can make the most
of this powerful feature.

### What is AOP and why should you care?
Aspect - Oriented programming allows you to keep cross - cutting concerns separate. This includes things like logging, security, and transaction management, which don't mix with your main business logic. Define behavior once instead of repeating them in your code. Then, declare where to use them.
For example, instead of adding transaction management to every service method:

```java
public void transferMoney(Account from, Account to, BigDecimal amount) {
    // Start transaction
    try {
        // Business logic
        from.withdraw(amount);
        to.deposit(amount);
        // Commit transaction
    } catch (Exception e) {
        // Rollback transaction
        throw e;
    }
}
```

You can focus on just the business logic:

```java
@Transactional
public void transferMoney(Account from, Account to, BigDecimal amount) {
    from.withdraw(amount);
    to.deposit(amount);
}
```
Spring handles the transaction management aspect through AOP. Clean, elegant, and DRY!

The proxy pattern - the foundation of Spring AOP
At its core, Spring AOP relies on the proxy pattern. A proxy is an object that stands in for another object,
controlling access to it. In Spring, these proxies catch method calls to your beans. They can act before, after,
or around the actual method runs.

Spring uses two types of proxies:
- JDK Dynamic proxies (the default for interface - based proxies).
- CGLIB proxies (used when proxying classes directly).

Let's examine how each works.

### JDK Dynamic Proxies
When your Spring bean implements an interface, Spring uses JDK's built - in dynamic proxy mechanism. The java.lang.reflect.Proxy class creates a proxy instance that implements the specified interfaces.
Here's how it works in simplified form:
```java
// The interface
public interface UserService {
    User findById(Long id);
}

// Your implementation
@Service
public class UserServiceImpl implements UserService {
    @Override
    public User findById(Long id) {
        // business logic
        return userRepository.findById(id);
    }
}

// What Spring creates behind the scenes (simplified)
UserService proxy = (UserService) Proxy.newProxyInstance(
    UserService.class.getClassLoader(),
    new Class<?>[] { UserService.class },
    new InvocationHandler() {
        private final UserService target = new UserServiceImpl();

        @Override
        public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
            // Before advice
            System.out.println("Before method: " + method.getName());

            try {
                // Actual method invocation
                Object result = method.invoke(target, args);

                // After returning advice
                System.out.println("Method completed successfully");
                return result;
            } catch (Exception e) {
                // After throwing advice
                System.out.println("Method threw an exception: " + e.getMessage());
                throw e;
            } finally {
                // After (finally) advice
                System.out.println("After method: " + method.getName());
            }
        }
    }
);
```

The key insight here is that Spring creates a dynamic proxy that implements the same interface(s) as your bean.
When code calls a method on this proxy, the invoke method steps in. It adds the aspect behavior and then passes
the call to your real impelementation.

### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/spring-aop-under-the-hood-how-proxies-work-9499fec7f0a2" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/spring-aop-under-the-hood-how-proxies?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/spring-aop-under-the-hood-how-proxies-work/"  >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)
