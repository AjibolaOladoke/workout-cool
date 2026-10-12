# workout-cool

## What This Is

This is part of the Swift Tech Co. working stack for product and engineering. It gathers the workout-cool notes, examples and fixes that keep delivery fast, and doubles as the reference map we hand to whoever picks up this thread next.

## Images

[![workout-cool](images/preview.png)](https://github.com/Swift-Tech-Co/workout-cool)

## Table of Contents

- [About](#about)
- [Project Origin & Motivation](#-project-origin--motivation)
- [Quick Start](#quick-start)
- [Exercise Database Import](#exercise-database-import)
- [Project Architecture](#project-architecture)
- [Contributing](#contributing)
- [Self-hosting](#deployment--self-hosting)
- [Resources](#resources)
- [License](#license)

## Contributors

<a href="https://github.com/Swift-Tech-Co/workout-cool">
  
</a>

## About

A comprehensive fitness coaching platform that allows create workout plans for you, track progress, and access a vast exercise database with
detailed instructions and video demonstrations.

## 🎯 Project Origin & Motivation

This project was born from a personal mission to revive and improve upon a previous fitness platform. As the **primary contributor** to the
original workout.lol project, I witnessed its journey and abandonment. 🥹

### The Story Behind **_workout.cool_**

- 🏗️ **Original Contributor**: I was the main contributor to workout.lol
- 💼 **Business Challenges**: The original project faced major hurdles with exercise video partnerships (no reliable video provider) could
  be established
- 💰 **Project Sale**: Due to these partnership issues, the project was sold to another party
- 📉 **Abandonment**: The new owner quickly realized that **exercise video licensing costs were prohibitively expensive**, began to be sick
  and abandoned the entire project
- 🔄 **Revival Attempts**: For the past **9 months**, I've been trying to reconnect with the new stakeholder
- 📧 **Radio Silence**: Despite multiple (15) attempts, there has been no response
- 🚀 **New Beginning**: Rather than let this valuable work disappear, I decided to create a fresh, modern implementation

### Why **_workout.cool_** Exists

**Someone had to step up.**

The opensource fitness community deserves better than broken promises and abandoned platforms.

I'm not building this for profit.

This isn't just a revival : it's an evolution. **workout.cool** represents everything the original project could have been, with the
reliability, modern approach, and **maintenance** that the fitness open source community deserves.

## 👥 From the Community, For the Community

**I'm not just a developer : I'm a user who refused to let our community down.**

I experienced firsthand the frustration of watching a beloved tool slowly disappear. Like many of you, I had workouts saved, progress
tracked, and a routine built around the platform.

### My Mission: Rescue & Revive.

_If you were part of the original workout.lol community, welcome back! If you're new here, welcome to the future of fitness platform
management._

## Quick Start

### Prerequisites

- Node.js (v18+)
- pnpm (v8+)
- Docker

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/Swift-Tech-Co/workout-cool
   cd workout-cool
   ```

2. **Choose your installation method:**

<details>
<summary><b>🐳 With Docker</b></summary>

### Docker Installation

1. **Copy environment variables**

   ```bash
   cp .env.example .env
   ```

2. **Start everything for development:**

   ```sh
   make dev
   ```

   - This will start the database in Docker, run migrations, seed the DB, and start the Next.js dev server.
   - To stop services run `make down`

3. **Open your browser** Navigate to https://github.com/Swift-Tech-Co/workout-cool

</details>

<details>
<summary><b>💻 Without Docker</b></summary>

### Manual Installation

1. **Install dependencies**

   ```bash
   pnpm install
   ```

2. **Copy environment variables**

   ```bash
   cp .env.example .env
   ```

3. **Set up PostgreSQL database**

   - If you don't already have it, install PostgreSQL locally
   - Create a database named `workout_cool` : `createdb -h localhost -p 5432 -U postgres workout_cool`

4. **Run database migrations**

   ```bash
   npx prisma migrate dev
   ```

5. **Seed the database (optional)**

See the - [Exercise database import section](#exercise-database-import)

6. **Start the development server**

   ```bash
   pnpm dev
   ```

7. **Open your browser** Navigate to https://github.com/Swift-Tech-Co/workout-cool

</details>

## Exercise Database Import

The project includes a comprehensive exercise database. To import a sample of exercises:

### Prerequisites for Import

1. **Prepare your CSV file**

Your CSV should have these columns:

```
id,name,name_en,description,description_en,full_video_url,full_video_image_url,introduction,introduction_en,slug,slug_en,attribute_name,attribute_value
```

You can use the provided example.

### Import Commands

```bash

## Project Architecture

This project follows **Feature-Sliced Design (FSD)** principles with Next.js App Router:

```
src/
├── app/ # Next.js pages, routes and layouts
├── processes/ # Business flows (multi-feature)
├── widgets/ # Composable UI with logic (Sidebar, Header)
├── features/ # Business units (auth, exercise-management)
├── entities/ # Domain entities (user, exercise, workout)
├── shared/ # Shared code (UI, lib, config, types)
└── styles/ # Global CSS, themes
```

### Architecture Principles

- **Feature-driven**: Each feature is independent and reusable
- **Clear domain isolation**: `shared` → `entities` → `features` → `widgets` → `app`
- **Consistency**: Between business logic, UI, and data layers

### Example Feature Structure

```
features/
└── exercise-management/
├── ui/ # UI components (ExerciseForm, ExerciseCard)
├── model/ # Hooks, state management (useExercises)
├── lib/ # Utilities (exercise-helpers)
└── api/ # Server actions or API calls
```

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Workflow

1. **Create an issue** for the feature/bug you want to work on. Say that you will work on it (or no)
2. Fork the repository
3. Create your feature|fix|chore|refactor branch (`git checkout -b feature/amazing-feature`)
4. Make your changes following our [code standards](#code-style)
5. Commit your changes (`git commit -m 'feat: add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request (one issue = one PR)

**📋 For complete contribution guidelines, see our [Contributing Guide](CONTRIBUTING.md)**

### Code Style

- Follow TypeScript best practices
- Use Feature-Sliced Design architecture
- Write meaningful commit messages

## Deployment / Self-hosting

> 📖 **For detailed self-hosting instructions, see our [Complete Self-hosting Guide](docs/SELF-HOSTING.md)**
>
> 📺 **You can also watch a 3-minute video guide on self-hosting Workout.Cool.**

To seed the database with the sample exercises, set the `SEED_SAMPLE_DATA` env variable to `true`.

### Using Docker

```bash
# Build the Docker image
docker build -t yourusername/workout-cool .

# Run the container
docker run -p 3000:3000 --env-file .env.production yourusername/workout-cool
```

### Using Docker Compose

#### DATABASE_URL

Update the `host` to point to the `postgres` service instead of `localhost`

```bash
docker compose up -d
```

### Manual Deployment

```bash
# Build the application
pnpm build

# Run database migrations
export DATABASE_URL="your-production-db-url"
npx prisma migrate deploy

# Start the production server
pnpm start
```

## Resources

- Feature-Sliced Design
- Next.js Documentation
- Prisma Documentation
- Better Auth

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 🤝 Join the Rescue Mission

**This is about rebuilding what we lost, together.**

### How You Can Help

- 💬 **Telegram** to connect with other fitness enthusiasts and developers
- 🐛 **Report issues** you find. I'm listening to every single one
- 💡 **Share your feature requests** finally, someone who will actually implement them !
- 🔄 **Spread the word** to fellow fitness enthusiasts who lost hope
- 🤝 **Contribute code** if you're a developer : let's build this together

<div align="center">
  <a href="https://t.me/+Qt_eFvkb2rliMzNh" target="_blank">
    
  </a>
  <br><br>
  <a href="https://github.com/Swift-Tech-Co/workout-cool" target="_blank">
    
  </a>
</div>

Appear in the README and on the website as supporter by donating:

<div align="center">
  <a href="https://github.com/Swift-Tech-Co/workout-cool" target="_blank">
  </a>
  &nbsp;&nbsp;&nbsp;
  <!-- TODO: setup -->
  <!-- <a href="https://github.com/Swift-Tech-Co/workout-cool" target="_blank">
  </a> -->
</div>

<p align="center" style="margin-top:20px;">
  <em>If you believe in open-source fitness tools and want to help this project thrive,<br>
</p>

<p align="center">
  Your support helps cover hosting costs, exercise database updates, and continuous improvement.<br>
  Thank you for keeping <strong>workout.cool</strong> alive and evolving 💪
</p>

<br />
<br />
<a href="https://github.com/Swift-Tech-Co/workout-cool">

</a>

---

## Swift Tech Co.

Built and maintained by Swift Tech Co.

AI Automation | FinTech Platforms | Custom Software and Mobile Apps | SaaS Platforms | Cloud Infrastructure | Cybersecurity | SEO and Marketing | API Integration

**Join our community on Telegram:** [t.me/+Qt_eFvkb2rliMzNh](https://t.me/+Qt_eFvkb2rliMzNh)

Home | Services | Careers | Referral Program | Influencers | About | Contact

**Connect**

- Website: https://github.com/Swift-Tech-Co/workout-cool
- LinkedIn: [linkedin.com/in/stephenoladoke](https://www.linkedin.com/in/stephenoladoke/)
- LinkedIn (Company): [linkedin.com/company/swift-tech-co](https://www.linkedin.com/company/swift-tech-co)
- X: [@MrOladoke](https://x.com/MrOladoke)
- Instagram: [@mr.oladoke](https://www.instagram.com/mr.oladoke/)
- Instagram (Company): [@swifttechco](https://www.instagram.com/swifttechco/)
- Organization: [github.com/Swift-Tech-Co](https://github.com/Swift-Tech-Co)

## Sources

Compiled and maintained from upstream [Snouzy/workout-cool](https://github.com/Snouzy/workout-cool) under permissive open-source license.

---

Maintained by [Swift Tech Co.](https://github.com/Swift-Tech-Co) - [Telegram](https://t.me/+Qt_eFvkb2rliMzNh)

## Sources

Compiled and maintained from upstream [Snouzy/workout-cool](https://github.com/Snouzy/workout-cool) under permissive open-source license.

---

Maintained by [Swift Tech Co.](https://github.com/Swift-Tech-Co) - [Telegram](https://t.me/+Qt_eFvkb2rliMzNh)