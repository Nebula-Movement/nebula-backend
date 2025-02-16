
# Nebula Backend

This repository contains the backend code for **[Nebula](https://www.nebula.xyz/)**, an AI-powered social platform built on the Movement blockchain. It provides API endpoints for managing generative AI prompts, user interactions, social features, and leaderboards, all designed to integrate with the Movement blockchain.

## 📋 Table of Contents

* [Overview](#-overview)
* [API Endpoints](#-api-endpoints)
  * [Prompt Marketplace Endpoints](#prompt-marketplace-endpoints)
  * [Leaderboard Endpoints](#leaderboard-endpoints)
  * [Social Feed Endpoints](#social-feed-endpoints)
* [Automation Tasks](#-automation-tasks)
* [Database](#-database)
* [Dependencies](#-dependencies)
* [Running the Application](#-running-the-application)

## 🤖 Overview

Nebula backend is built using FastAPI and interacts with a database (PostgreSQL) to store and manage indexed data from the Movement blockchain related to AI prompts, user activity, and leaderboards. 

## 🤖 API Endpoints

### Prompt Marketplace Endpoints

* **POST `/add-premium-prompts`:** Adds a new premium prompt to the marketplace. These premium prompts are linked to NFTs on the Aptos blockchain.
* **GET `/get-premium-prompts`:** Retrieves all premium prompts.
* **GET `/premium-prompt-filters`:**  Gets all available filters for premium prompts (e.g., recent, popular, trending).
* **POST `/filter-premium-prompts`:** Filters premium prompts based on the provided filter type.
* **POST `/add-public-prompts`:** Adds a new public prompt.
* **GET `/prompt-tags`:** Retrieves all available prompt tags.
* **GET `/get-public-prompts`:** Retrieves all public prompts.
* **POST `/filter-public-prompts`:** Filters public prompts based on tag and visibility.

### Leaderboard Endpoints

* **GET `/generations-24h`:**  Leaderboard based on the number of generations in the last 24 hours. This tracks the usage of prompts or the creation of AI-generated content.
* **GET `/streaks`:** Leaderboard based on consecutive days with generations, encouraging user engagement.
* **GET `/xp`:** Leaderboard based on user XP earned through frequent activities on the platform.

### Social Feed Endpoints

* **POST `/like-prompt`:** Likes a public or premium prompt.
* **POST `/comment-prompt`:** Adds a comment to a prompt.
* **GET `/get-prompt-comments`:** Retrieves comments for a prompt.
* **POST `/follow-creator`:**  Follows a creator.
* **DELETE `/unfollow-creator`:** Unfollows a creator.
* **GET `/creator-followers`:** Gets a list of followers for a creator.
* **GET `/user-following`:** Gets a list of creators a user is following.
* **GET `/feed`:** Retrieves the social feed for a user (prompts from followed creators and new creators).
* **GET `/feed/followers`:** Gets a feed of prompts from the user's followers.
* **GET `/feed/following`:** Gets a feed of prompts from the creators the user is following.
* **GET `/feed/combined`:** Gets a combined feed from followers and following.
* **GET `/prompt-likes`:** Retrieves the number of likes for a prompt and whether the user has liked it.


## 🤖 Database

The Nebula backend uses a database (PostgreSQL) to store:

* Prompts (public and premium)
* User interactions (likes, comments, follows)
* User statistics (for leaderboards)

## 🤖 Dependencies

The project uses the following key dependencies:

* FastAPI
* SQLAlchemy
* Celery
* Requests

## 🤖 Running the Application

1. **Install dependencies:** `pip install -r requirements.txt`
2. **Configure environment variables:** Set the required environment variables (e.g., database connection string, API keys, Aptos node URL).
3. **Run the FastAPI application:** `uvicorn app.main:app --reload`
4. **Start the Celery worker:** `celery -A app.celery.celery.celery_app worker --loglevel=info`
5. **Start the Celery beat scheduler:** `celery -A app.celery.celery.celery_app beat --loglevel=info`
