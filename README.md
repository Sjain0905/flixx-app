<div align="center">

# 🎬 Flixx

**Discover movies and TV shows — powered by TMDB, built in pure JavaScript.**

[![Made with JavaScript](https://img.shields.io/badge/JavaScript-ES2017+-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![TMDB API](https://img.shields.io/badge/API-TMDB-01d277?logo=themoviedatabase&logoColor=white)](https://www.themoviedb.org/documentation/api)
[![No Framework](https://img.shields.io/badge/Framework-None-blueviolet)](https://claude.ai/chat/9c6283bd-78b7-40fc-8d83-a8b8a25813be#tech-stack)

</div>

---

## ✨ Overview

**Flixx** is a movie and TV show discovery app built with vanilla JavaScript, HTML, and CSS — no framework, no build step, no dependencies beyond a couple of lightweight UI libraries. It pulls live data from [The Movie Database (TMDB)](https://www.themoviedb.org/) to bring you now-playing movies, trending TV shows, rich detail pages, and fast, paginated search.

It was built as a deep-dive into the fundamentals — DOM manipulation, the Fetch API, `async`/`await`, and simple client-side routing — without a framework doing the heavy lifting.

## Live Demo / Screenshots

_(Add a deployed link and screenshots here — e.g. via GitHub Pages, Netlify, or Vercel)_

## 🚀 Features

🎞️ **Now Playing Carousel**
An auto-playing Swiper.js slider showcasing movies currently in theaters, with responsive breakpoints for mobile through desktop.

🔥 **Popular Movies & TV Shows**
Fresh, always-up-to-date grids of the top 20 trending titles.

📄 **Rich Detail Pages**
Poster, rating, overview, genres, and a cinematic backdrop for every movie and show — plus budget/revenue and runtime for movies, and episode count/status for TV.

🔍 **Smart Search with Pagination**
Search movies or TV shows by keyword, toggle between the two, and page through results with Prev/Next controls synced to the API's total result count.

⏳ **Loading & Error States**
A loading spinner during API calls, and clear on-screen alerts for empty searches or failed requests.

🔐 **Secure API Key Handling**
The TMDB key lives in a local, git-ignored file — never committed to source control.

📱 **Fully Responsive**
CSS Grid–based layouts and Swiper breakpoints adapt smoothly from phone to desktop.

## 🛠️ Tech Stack

Layer
Tools

Structure
Plain HTML5 (one file per page/route)

Styling
Plain CSS3 (Flexbox + Grid), Google Fonts (Poppins)

Behavior
Vanilla JavaScript (ES2017+ `async`/`await`, template literals, `fetch`)

Data
[TMDB API v3](https://developer.themoviedb.org/reference/intro/getting-started)

UI libraries
[Swiper.js](https://swiperjs.com/) (carousel), [Font Awesome](https://fontawesome.com/) (icons)

No package manager, bundler, or framework required — the whole app runs as static files.

## 📁 Project Structure

```
flixx-app/
├── index.html          # Home — now-playing slider + popular movies
├── shows.html           # Popular TV shows grid
├── movie-details.html   # Single movie detail page (?id=<movieId>)
├── tv-details.html      # Single TV show detail page (?id=<showId>)
├── search.html           # Search results + pagination
├── js/
│   ├── env.js            # (git-ignored, you create this) — sets window.env.TMDB_API_KEY
│   └── script.js         # All app logic: API calls, rendering, routing, events
├── css/
│   ├── style.css         # Layout, typography, components
│   └── spinner.css       # Loading spinner styles
├── lib/                  # Vendored third-party libraries
│   ├── swiper.js / swiper.css
│   └── fontawesome.css
├── webfonts/              # Font Awesome icon fonts
├── images/                 # Fallback image + hero background
├── .env.example             # Template showing the expected env var name
└── .gitignore                # Excludes .env and js/env.js from version control
```

## ⚙️ How It Works

A single JS entry point (`js/script.js`) is shared across every page. On load, `init()` checks `window.location.pathname` and calls the function relevant to that page — a lightweight, hand-rolled router:

```
switch (global.currPage) {
  case '/':
  case '/index.html': displaySlider(); popularMovies(); break;
  case '/shows.html': popularShows(); break;
  case '/movie-details.html': movieDetails(); break;
  case '/tv-details.html': showDetails(); break;
  case '/search.html': search(); break;
}
```

A shared `global` object holds app-wide state — the current page, in-progress search params, and API config (with the key pulled from `window.env.TMDB_API_KEY`). Every network call flows through two helpers, `fetchAPIData()` and `searchAPIData()`, which handle the spinner, error checking, and graceful fallbacks in one place.

## 🏁 Getting Started

Flixx is a static site with zero build step — run it with any local static server:

```
git clone https://github.com/Sjain0905/flixx-app.git
cd flixx-app

# Option 1: VS Code Live Server extension — right-click index.html → "Open with Live Server"

# Option 2: Python
python3 -m http.server 5500

# Option 3: npx
npx serve .
```

Then open `http://localhost:5500` (or whichever port your server uses).

### 🔑 API Key Setup

The TMDB API key is **not** committed to this repo — it's read at runtime from `window.env.TMDB_API_KEY`.

1. Create a free account at [themoviedb.org](https://www.themoviedb.org/) and generate an API key under **Settings → API**.
2. Check `.env.example` for the expected variable name.
3. Create `js/env.js` in the project root with:

```
window.env = {  TMDB_API_KEY: 'your_tmdb_api_key_here',};
```

4. `js/env.js` is already wired up to load before `js/script.js` in every page — no further changes needed.

## 🙏 Acknowledgements

- Data provided by [The Movie Database (TMDB)](https://www.themoviedb.org/) — this product uses the TMDB API but is not endorsed or certified by TMDB.
- Carousel powered by [Swiper](https://swiperjs.com/).
- Icons by [Font Awesome](https://fontawesome.com/).
