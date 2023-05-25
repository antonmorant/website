---
layout: page
title: OneHaiku
index: 4
description:  Daily haikus delivered to your phone (iOS). Personal project.
---

## The app

OneHaiku is a minimalistic iOS app created with the goal of building and releasing an app from scratch. Developed as a one-man project, it has turned out to be a unique learning opportunity as I actively continue working on it.

Every day, users can open OneHaiku to unveil a carefully curated haiku poem individually picked for them. The design and functionality of the app are inspired by zen simplicity, allowing users to savor the beauty of the moment and then let go and continue about their day. This creates a small space for mindfulness and reflection in their daily lives.

All haikus are 100% human-made and authored by myself. The app invites feedback through the ability to rate haikus, which allows enhacing future selections as well as guiding the development of new content. This makes OneHaiku not only a technical endeavor but also a personal artistic outlet.

{: .featured-video }
{% include video.html filename="onehaiku_preview.mp4" %}

## Technical details

### Frontend
The front-end is built with Swift and UIKit. I originally started the app using SwiftUI, but in agreement with what I perceive to be the general community consensus, SwiftUI is not quite fully mature yet. While some of the features were really pleasant to work with (layouts, previews), I found the framework simply did not support creating animations with the level of complexity and control the project required. The initialy prototype was therefore rewritten into UIKit, which was a surprisingly easy transition. Today I am quite satisfied with this choice.

Additional details:
- Programmatic UI: Using SnapKit for autolayout.
- Programmatic animations: Instead of a 3rd-party tool, I took this opportunity to familiarize myself with vanilla iOS animations. The app uses UIView and CoreAnimation layer animations.
- Haptics: Given the deliberate simplicity of the app's functionality, animations & haptics play a key role in making the haiku reveal moment feel special.
- Asynchronous functions: After trying out various alternatives, async/await/throws turned out to be the most natural for the networking layer's API.
- User accounts: The app deliberately does not have an onboarding or signup flow. When the user first oppens the app, a user account is automatically created for them and credentials are stored for future authentication (which also happens transparently). Logout/login functionality will be added in the future.
- Crash reporting: Using Sentry for crash & error reporting.
- Caching: While the app requires backend connectivity to request a new haiku each day, it does cache it locally so that it's available bewtween app opens.

### Backend
The backend is built with Ruby on Rails. Cloud deployment and resources, including web server machines and a Postgres database, were initially managed with Heroku and later migrated to Fly.io. The backend's main responsibilities are creation and authentication of users, selection of haikus, and storing haiku ratings.

The rails app provides a REST API that allows to create and authenticate users, get a user's haiku for the day, and submit and update ratings. It also serves miscellaneous static pages requried for App Store publishing (e.g. the app's privacy policy or customer support details).

To support a password-less flow, when the client creates a user account it receives an authentication token that does not expire. This token is stored locally and can be used to authenticate with the backend, which will return an access token. This is a JWT (JSON Web Token) that encodes the user id as well as the expiration date (5-minute TTL), and is cryptographically signed by the backend using a public/private key pair. The client caches the access token, uses it on all authenticated requests, and refreshes it on expiration.

Additional details:
- Environments: Production and staging environments are kept separate to facilitate QA testing. Client debug builds use staging, while release builds use production.
- Continuous integration: Unit tests (RSpec) and linting (RuboCop) are automated via GitHub Actions.
- Security: The backend app admits only HTTPS connections and uses a custom domain with the corresponding TSL certificates.
- Error reporting: Using sentry for error reporting and performance monitoring.
- Admin dashboard: The backend uses ActiveAdmin to provide an administration dashboard in order to easily create haikus and monitor basic user activity. For instance, it displays the top 5 users by count of seen haikus together with the total count of haikus. This ensures new content continues to be created timely and users don't see repeated haikus.


## Release status
The app is currently in closed beta, distributed via TestFlight. Public release pending - watch this space for updates!
