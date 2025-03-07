# 🎬 React Movie App (TMDB API & Appwrite Integration)

## 📌 Overview
This is a **React-based Movie Application** that allows users to **browse, search, and discover movies** using data from [The Movie Database (TMDB)](https://www.themoviedb.org/). The app provides an intuitive interface to find popular movies, search for specific titles, and display movie details. Additionally, it integrates **Appwrite** to track the number of searches per movie and showcase the most searched movies in the **Trending Movies** section.

## 🚀 Features
✅ Fetch and display **popular movies** from TMDB.  
✅ **Search movies** dynamically using TMDB API.  
✅ Display **movie details** (title, overview, etc.).  
✅ Store search statistics in **Appwrite** and showcase **Trending Movies**.  
✅ Handle **loading** and **error states** gracefully.  
✅ **Optimized API calls** using React Hooks (`useState`, `useEffect`).

## 🛠️ Tech Stack
- **React.js** (Functional Components & Hooks)
- **TMDB API** (Movie data provider)
- **Appwrite** (Database & Backend Services)
- **Fetch API / Async-Await** (API calls)
- ** Tailwind CSS** (Styling)

## 📂 Project Structure
```
📦 movie-app
├── 📂 src
│   ├── 📂 components
│   │   ├── Search.js  # Search Component
│   ├── 📂 pages
│   │   ├── App.js     # Main App Component
│   ├── 📜 index.js    # Entry point
├── 📜 .env            # Environment Variables
├── 📜 package.json    # Dependencies & Scripts
└── 📜 README.md       # Project Documentation
```

## 🔧 Setup Instructions
### 1️⃣ Clone the Repository
```sh
git clone https://github.com/hellboy8/movie-app.git
cd movie-app
```
### 2️⃣ Install Dependencies
```sh
npm install
```
### 3️⃣ Set Up TMDB API Key
Create a `.env` file in the root folder and add your TMDB API key:
```sh
VITE_TMDB_API_KEY=your_tmdb_api_key_here
```

### 4️⃣ Set Up Appwrite
- Sign up on [Appwrite](https://appwrite.io/).
- Create a **database** to store movie search statistics.
- Generate an **Appwrite API Key** and add it to `.env`:
```sh
VITE_APPWRITE_PROJECT_ID=your_project_id
VITE_APPWRITE_API_KEY=your_api_key_here
VITE_APPWRITE_ENDPOINT=your_appwrite_endpoint
```

### 5️⃣ Run the Application
```sh
npm run dev
```

## 📜 API Integration
### Fetch Popular Movies
```js
const API_BASE_URL = 'https://api.themoviedb.org/3';
const API_KEY = import.meta.env.VITE_TMDB_API_KEY;

const fetchMovies = async () => {
  try {
    const response = await fetch(`${API_BASE_URL}/discover/movie?sort_by=popularity.desc`, {
      method: 'GET',
      headers: {
        accept: 'application/json',
        Authorization: `Bearer ${API_KEY}`,
      },
    });
    const data = await response.json();
    return data.results;
  } catch (error) {
    console.error('Error fetching movies:', error);
  }
};
```

### Search Movies & Update Trending in Appwrite
```js
const searchMovies = async (query) => {
  if (!query) return;
  try {
    const response = await fetch(`${API_BASE_URL}/search/movie?query=${query}`, {
      method: 'GET',
      headers: {
        accept: 'application/json',
        Authorization: `Bearer ${API_KEY}`,
      },
    });
    const data = await response.json();
    
    // Update search count in Appwrite
    await updateTrendingMovies(query);
    
    return data.results;
  } catch (error) {
    console.error('Error searching movies:', error);
  }
};

const updateTrendingMovies = async (movieTitle) => {
  try {
    await appwriteDatabase.createDocument('trendingMovies', movieTitle, { count: 1 });
  } catch (error) {
    console.error('Error updating trending movies:', error);
  }
};
```

## 🏗️ Future Enhancements
🚀 Add **Movie Details Page** with full movie information.  
🎨 Improve UI/UX with **better design & animations**.  
📱 Make it **mobile-responsive**.  
📝 Add **user reviews & ratings** feature.  
📊 Display **Trending Movies Graphs & Insights** using Appwrite.

## 📜 License
This project is **MIT Licensed**. Feel free to use and modify it.

---
🔗 **Developed by [Dhruv]**  
🎬 **Powered by [The Movie Database API](https://www.themoviedb.org/) & Appwrite**

