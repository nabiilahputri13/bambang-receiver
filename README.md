# BambangShop Receiver App ⋆౨ৎ˚⟡˖ ࣪
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a Rocket web framework skeleton that you can work with.

As this is an Observer Design Pattern tutorial repository, you need to implement a feature: `Notification`.
This feature will receive notifications of creation, promotion, and deletion of a product, when this receiver instance is subscribed to a certain product type.
The notification will be sent using HTTP POST request, so you need to make the receiver endpoint in this project.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Receiver" folder.

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    ROCKET_PORT=8001
    APP_INSTANCE_ROOT_URL=http://localhost:${ROCKET_PORT}
    APP_PUBLISHER_ROOT_URL=http://localhost:8000
    APP_INSTANCE_NAME=Safira Sudrajat
    ```
    Here are the details of each environment variable:
    | variable                | type   | description                                                     |
    |-------------------------|--------|-----------------------------------------------------------------|
    | ROCKET_PORT             | string | Port number that will be listened by this receiver instance.    |
    | APP_INSTANCE_ROOT_URL   | string | URL address where this receiver instance can be accessed.       |
    | APP_PUUBLISHER_ROOT_URL | string | URL address where the publisher instance can be accessed.       |
    | APP_INSTANCE_NAME       | string | Name of this receiver instance, will be shown on notifications. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)
3.  To simulate multiple instances of BambangShop Receiver (as the tutorial mandates you to do so),
    you can open new terminal, then edit `ROCKET_PORT` in `.env` file, then execute another `cargo run`.

    For example, if you want to run 3 (three) instances of BambangShop Receiver at port `8001`, `8002`, and `8003`, you can do these steps:
    -   Edit `ROCKET_PORT` in `.env` to `8001`, then execute `cargo run`.
    -   Open new terminal, edit `ROCKET_PORT` in `.env` to `8002`, then execute `cargo run`.
    -   Open another new terminal, edit `ROCKET_PORT` in `.env` to `8003`, then execute `cargo run`.

## Mandatory Checklists (Subscriber)
-   [ ✔ ] Clone https://gitlab.com/ichlaffterlalu/bambangshop-receiver to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [ ✔ ] Commit: `Create Notification model struct.`
    -   [ ✔ ] Commit: `Create SubscriberRequest model struct.`
    -   [ ✔ ] Commit: `Create Notification database and Notification repository struct skeleton.`
    -   [ ✔ ] Commit: `Implement add function in Notification repository.`
    -   [ ✔ ] Commit: `Implement list_all_as_string function in Notification repository.`
    -   [ ✔ ] Write answers of your learning module's "Reflection Subscriber-1" questions in this README.
-   **STAGE 3: Implement services and controllers**
    -   [ ✔ ] Commit: `Create Notification service struct skeleton.`
    -   [ ✔ ] Commit: `Implement subscribe function in Notification service.`
    -   [ ✔ ] Commit: `Implement subscribe function in Notification controller.`
    -   [ ✔ ] Commit: `Implement unsubscribe function in Notification service.`
    -   [ ✔ ] Commit: `Implement unsubscribe function in Notification controller.`
    -   [ ✔ ] Commit: `Implement receive_notification function in Notification service.`
    -   [ ✔ ] Commit: `Implement receive function in Notification controller.`
    -   [ ✔ ] Commit: `Implement list_messages function in Notification service.`
    -   [ ✔ ] Commit: `Implement list function in Notification controller.`
    -   [ ✔ ] Write answers of your learning module's "Reflection Subscriber-2" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Subscriber) Reflections

#### Reflection Subscriber-1
1. In this tutorial, we used RwLock<> to synchronise the use of Vec of Notifications. Explain why it is necessary for this case, and explain why we do not use Mutex<> instead?
Ans:

    We use RwLock to manage access to the list of notifications. It's like having a shared resource (the list) that multiple people (threads) want to use. RwLock allows many threads to read the list at once, but only one thread can write to it at a time. This is useful because reading happens a lot more often than writing, so it keeps things efficient and prevents conflicts between threads.

    We don't use Mutex because it's like having a lock with only one key. With Mutex, only one person (thread) can access the list at a time, whether they're reading or writing. This could cause a lot of waiting around, especially when many threads want to read the list. RwLock's approach is more flexible and better suited to our needs.

2. In this tutorial, we used lazy_static external library to define Vec and DashMap as a “static” variable. Compared to Java where we can mutate the content of a static variable via a static function, why did not Rust allow us to do so?
Ans:

    Rust doesn't allow mutating the content of static variables directly because it prioritizes safety and thread-safety. In Rust, static variables are immutable by default to prevent data races and ensure memory safety.

    By disallowing direct mutation of static variables, Rust encourages safer concurrency patterns. Instead, Rust provides mechanisms like Mutex, RwLock, or atomic types to safely mutate shared state in a concurrent environment. This approach helps prevent common concurrency bugs like data races, making Rust programs more reliable and easier to reason about.

    While it may seem restrictive compared to languages like Java, where mutating static variables is allowed, Rust's approach aligns with its core principles of safety, concurrency, and performance. It encourages developers to write code that is less prone to concurrency bugs and easier to maintain in the long run.

#### Reflection Subscriber-2

Step 31-32

    I don't think all the notifications appear correctly, when I try subscribing to different product types, some of the receiver instances shows the same product id.


1. Have you explored things outside of the steps in the tutorial, for example: src/lib.rs? If not, explain why you did not do so. If yes, explain things that you have learned from those other parts of code.
Ans:

    No, I have not. This week was so packed with lebaran and other assignments so I haven't had time for it.

2. Since you have completed the tutorial by now and have tried to test your notification system by spawning multiple instances of Receiver, explain how Observer pattern eases you to plug in more subscribers. How about spawning more than one instance of Main app, will it still be easy enough to add to the system?
Ans:

    The Observer pattern simplifies adding more subscribers by letting us plug them in without changing existing code. Each subscriber can register independently, making it flexible and scalable.

    Spawning more than one instance of the main app is also manageable. Each instance acts as a publisher, notifying subscribers independently, allowing for parallel processing and scalability. It can remains manageable and scalable, as each instance operates independently and can handle its own set of notifications and subscribers.

3. Have you tried to make your own Tests, or enhance documentation on your Postman collection? If you have tried those features, tell us whether it is useful for your work (it can be your tutorial work or your Group Project).
Ans:

    Yes, I have. Creating tests in Postman is definitely useful for automated testing of APIs, which can help ensure the correctness and reliability of the endpoints. It's useful for verifying that the API behaves as expected under various conditions and can catch bugs or regressions early in the development process.