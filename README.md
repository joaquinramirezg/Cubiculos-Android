# Study room booking: Android client

> University project (UTEC, 2020). An Android app for reserving study rooms on campus, built with [Victor Ostolaza](https://github.com/vostolaza).

Live portfolio: [joaquinramirez.dev](https://joaquinramirez.dev/)

## The problem

Study rooms at UTEC were claimed in person and on paper, which meant students walked across campus to find every room taken, and rooms sat empty when whoever booked them did not show up. The idea was to let students see real availability for a given day and reserve a slot from their phone.

## What is in this repository

The **Android client only**. The Flask web application and its database ran alongside it as a separate project and were never published, so this repo is the mobile half of the system.

The client is a thin, honest REST consumer, and its calls document the API contract we designed:

| Endpoint | Purpose |
|---|---|
| `POST /signup`, `POST /authenticate`, `GET /logout` | account creation and session handling |
| `GET /available/<date>` | rooms still free on a given day |
| `POST /make-reservation` | claim a slot |
| `GET /my-reservations/<user>` | a student's own bookings |

## How it works

Ten activities cover the whole flow: sign up, log in, pick a day, browse what is available, reserve, and review your own reservations. `Volley` handles the HTTP calls, and two `RecyclerView` adapters render the availability and reservation lists. Session state is kept client side and cleared on logout.

## Stack

Java, Android SDK (minSdk 19, compileSdk 30), Volley, Gradle. The backend it talks to was Flask with a SQL database, deployed on an Ubuntu instance on AWS.

## Status and limitations

This is a 2020 coursework project, unmaintained since, and it is worth being clear about what that means:

- The committed base URL is `http://10.0.2.2:8080`, which is the Android emulator's alias for the host machine. The app therefore expects a backend running locally and will not connect to anything on its own.
- Traffic is plain HTTP with no TLS, and credentials are posted directly. Fine behind an emulator on a laptop, not acceptable anywhere real.
- There are no tests, and the SDK targets are five years stale.

It worked end to end on campus at the time, which was the point of the assignment. My production work since then is written up at [joaquinramirez.dev](https://joaquinramirez.dev/).
