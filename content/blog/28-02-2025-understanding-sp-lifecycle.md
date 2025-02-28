---
title: Understanding Spring Beab Lifecycle
type: blog
sidebar:
  open: true
date: 2025-02-28
comments: true
---

![Beans](/images/2025-02-28-bean-lifecycle/beans.png "Coffee beans, but today about different beans")

### Introduction
The Spring Framework is key for Java enterprise development. It manages "beans," which are objects, using a smart lifecycle system.
It's important for developers to grasp this lifecycle in Spring applications. This knowledge gives them control over how resources are set up,
how they behave, and how to clean them up properly.

In this article, we'll look at the Spring bean lifecycle. We'll discuss how beans are created and destroyed.
We'll cover both theory and practical examples. In the end, you'll grasp how Spring handles beans. You'll learn
how to use lifecycle hooks to boost your applications.
### The Spring Bean lifecycle phases
The Spring bean lifecycle can be divided into several distinct phases:
1. Bean definition loading
2. Bean instantiation
3. Populating properties
4. BeanNameAware and BeanFactoryAware callbacks
5. Pre-initialization
6. InitializingBean and custom init methods
7. Post-initialization (BeanPostProcessor)
8. Bean is ready for use
9. DisposableBean and custom destroy methods

Let's examine each of these phases in detail.

#### 1. Bean definition loading
Spring begins by loading bean definitions. It uses XML files, Java annotations or Java configuration clasess.
```java
@Configuration
public class AppConfig {
    @Bean
    public UserService userService() {
        return new UserServiceImpl();
    }
}
```

#### 2. Bean instantiation
Spring creates an instance of the bean using one of several mechanisms:
```javapublic class UserServiceImpl implements UserService {
    public UserServiceImpl() {
        System.out.println("UserServiceImpl instantiated!");
    }
}
```
#### 3. Populating properties
```java
@Service
public class UserServiceImpl implements UserService {
    private final UserRepository userRepository;

    @Autowired
    public UserServiceImpl(UserRepository userRepository) {
        this.userRepository = userRepository;
        System.out.println("Dependencies injected!");
    }
}
```
#### 4. Awareness interfaces
Spring calls specific interface methods if the bean implements awareness interfaces.
```java
@Service
public class UserServiceImpl implements UserService, BeanNameAware, BeanFactoryAware {
    private String beanName;
    private BeanFactory beanFactory;

    @Override
    public void setBeanName(String name) {
        this.beanName = name;
        System.out.println("Bean name set: " + name);
    }

    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        this.beanFactory = beanFactory;
        System.out.println("BeanFactory set");
    }
}
```
5–7. Pre-initialization, Initialization and post-initilization
These phases handle bean initialization through callbacks and custom methods.


### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/understanding-spring-bean-lifecycle-ee0781ab7368" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/understanding-spring-bean-lifecycle?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/understanding-spring-bean-lifecycle/"  >}}
{{< /cards >}}
