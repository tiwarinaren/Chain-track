# ChainTrack - Habit Tracker

A simple, shareable habit tracker focused on building streaks ('chains') for two users. Built with HTML, Tailwind CSS, JavaScript, and Firebase Realtime Database for seamless synchronization.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Link to Live Demo](YOUR_DEMO_URL_HERE)** *(Replace with your actual demo URL if deployed)*

## Screenshots

*(Consider adding screenshots here to showcase the application's UI. Good examples include: Login Screen, User Habit View (with chains), Comparison Dashboard, Settings Panel)*

![Screenshot Placeholder 1](IMAGE_URL_1_HERE)
![Screenshot Placeholder 2](IMAGE_URL_2_HERE)
![Screenshot Placeholder 3](IMAGE_URL_3_HERE)

## Features

*   **Two-User Tracking:** Designed for simple sharing between two users (e.g., partners, friends).
*   **Habit Creation & Tracking:** Easily add new habits and track daily completion with a single click.
*   **Streak Visualization:** See your current habit chains visually.
*   **Streak Calculation:** Automatically calculates current and best streaks for each habit.
*   **Comparison Dashboard:** View a side-by-side comparison of key stats and current streaks for shared habits between users.
*   **Notes:** Add optional short notes to daily habit entries.
*   **Categories:** Assign categories to habits for organization (automatically color-coded).
*   **Completion Rate:** Calculates the overall completion percentage for each habit.
*   **Dark/Light Mode:** Toggle between themes, remembers preference locally.
*   **PIN Lock:** Simple 4-digit PIN protection for local device access (PIN is not synced).
*   **Real-time Sync:** Uses Firebase Realtime Database to instantly sync habit data, names, and avatars across devices/browsers logged into the same shared data.
*   **Data Management:** Edit habit names/categories, manually edit the streak chain, reset individual habit chains, or reset all data for both users.
*   **User Profiles:** Set custom names and upload avatar images for each user.
*   **"Add to Home Screen" (PWA-like):** Optimized for adding to your mobile home screen for a native app feel (especially on iOS using meta tags).
*   **Responsive Design:** Usable on various screen sizes.
*   **Motivational Quotes:** Displays a different motivational quote on each load.
*   **Animations:** Subtle animations for UI elements and a confetti celebration for tracking a habit.

## Tech Stack

*   **Frontend:** HTML5, CSS3, JavaScript (ES6+)
*   **CSS Framework:** [Tailwind CSS](https://tailwindcss.com/) v3
*   **Database:** [Firebase Realtime Database](https://firebase.google.com/products/realtime-database) (using v9 Compat SDK)
*   **Charting:** [Chart.js](https://www.chartjs.org/)
*   **Icons:** [Font Awesome](https://fontawesome.com/)
*   **Animations:** [Anime.js](https://animejs.com/), [Canvas Confetti](https://github.com/catdad/canvas-confetti)

## Setup and Installation

To run this project locally or deploy your own instance:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/chaintrack.git # Replace with your repo URL
    cd chaintrack
    ```

2.  **Firebase Setup:**
    *   Create a new project on the [Firebase Console](https://console.firebase.google.com/).
    *   In your Firebase project, go to **Build** -> **Realtime Database**. Click "Create database" and choose a region (e.g., `us-central1`, `asia-southeast1` - note the region used in your `databaseURL`). Start in **test mode** for initial setup (remember to secure rules later).
    *   Go to **Project settings** (gear icon) -> **General**. Scroll down to "Your apps".
    *   Click the Web icon (`</>`) to register a new web app.
    *   Give it a nickname (e.g., "ChainTrack Web").
    *   **Do NOT** set up Firebase Hosting at this stage unless you intend to use it for deployment.
    *   After registration, Firebase will provide you with a configuration object (`firebaseConfig`). **Copy these values.**

3.  **Configure Firebase Credentials:**
    *   In the root directory of the cloned project, find the file `firebase-config.example.js`.
    *   **Rename** or **copy** this file to `firebase-config.js`.
    *   **Edit `firebase-config.js`** and paste the configuration values you copied from the Firebase console. It should look like this:
        ```javascript
        // --- Firebase Configuration ---
        // IMPORTANT: This file contains your actual Firebase keys.
        // DO NOT COMMIT THIS FILE TO GITHUB. Ensure it's listed in .gitignore.

        const firebaseConfig = {
            apiKey: "AIza...", // YOUR ACTUAL KEY
            authDomain: "your-project-id.firebaseapp.com",
            databaseURL: "https://your-project-id-default-rtdb.your-region.firebasedatabase.app", // ENSURE THIS IS CORRECT
            projectId: "your-project-id",
            storageBucket: "your-project-id.appspot.com",
            messagingSenderId: "123...",
            appId: "1:123...:web:abc...",
            measurementId: "G-..." // Optional
        };
        ```
    *   **Crucially:** The `firebase-config.js` file is listed in `.gitignore` and **should NOT be committed to your public repository** as it contains sensitive API keys. The example file is safe to commit.

4.  **Create Icons:**
    *   Create a square PNG icon (180x180 or 192x192 pixels) with a solid background for the iOS home screen. Save it as `apple-touch-icon.png` in the root directory.
    *   (Optional) Create `favicon.ico` and `icon.svg` for browser tabs and place them in the root.

5.  **Run Locally:**
    *   Since this is a static HTML/JS/CSS application, you can often open the `code (2).html` (or `index.html` if you rename it) file directly in your browser.
    *   For features like service workers (if added later) or certain APIs, you might need a simple local server. You can use tools like VS Code's "Live Server" extension or Python's built-in server:
        ```bash
        # Navigate to the project directory in your terminal
        python -m http.server
        # Then open http://localhost:8000 (or the port specified) in your browser
        ```

6.  **Deploy:**
    *   Deploy the contents of the project directory (HTML, CSS, JS, `firebase-config.js`, icons) to any static web hosting provider (e.g., GitHub Pages, Netlify, Vercel, Firebase Hosting).

## Security Considerations

*   **API Keys:** Firebase API keys for web apps are **designed to be public**. They identify your Firebase project but don't grant automatic access.
*   **Firebase Security Rules:** **Security is primarily enforced by Firebase Security Rules.** You **MUST** configure rules for your Realtime Database to prevent unauthorized access. Go to your Firebase Console -> Realtime Database -> Rules. **Do not leave the rules as public (`".read": true, ".write": true`) in a production environment.** Define rules that appropriately restrict read/write access (e.g., based on user authentication if you add it later, or perhaps a shared secret if absolutely necessary, although less secure).
*   **Firebase App Check:** Consider enabling [Firebase App Check](https://firebase.google.com/docs/app-check) for an additional layer of security to verify requests are coming from your legitimate app instance.

## PWA / Add to Home Screen

*   The app uses meta tags (`apple-mobile-web-app-capable`, etc.) to enable the "Add to Home Screen" feature on iOS, allowing it to run in a standalone, app-like window.
*   A PNG icon (`apple-touch-icon.png`) is used for the iOS home screen icon for best compatibility.
*   HTTPS is required for PWA features.
*   A `manifest.json` file was previously used but removed as it caused issues with iOS standalone mode in testing. It could potentially be added back (carefully configured, possibly using PNG icons instead of Base64 SVGs) if enhanced Android PWA features (like install prompts, splash screens) are desired.

## Future Enhancements (Ideas)

*   Firebase Authentication for proper user accounts instead of just two fixed users.
*   More detailed statistics and charts (e.g., monthly views, habit success rates over time).
*   Data export/import functionality.
*   Customizable reminders/notifications.
*   Ability to reorder habits.
*   Support for different habit types (e.g., numerical, timed).

## Contributing

Contributions are welcome! Please feel free to fork the repository, make changes, and submit a pull request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file (or add the MIT license text directly here if you don't have a separate file) for details.
