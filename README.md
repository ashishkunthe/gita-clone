# README.md

## Bhagavad Gita – Chapter Page (Svelte UI Recreation)

This project is a recreation of the webpage at
[https://sanskrit.ie/gita.php](https://sanskrit.ie/gita.php)
as required in Round 2 of the assignment.
The objective was to replicate the UI, layout, responsiveness, and interactivity using Svelte, without access to original design files or source code.

API integration will be added once the API details are provided.

---

## Live Demo

**Hosted URL:**https://gita-clone-seven.vercel.app/

## GitHub Repository

**Repository:** (https://github.com/ashishkunthe/gita-clone)

---

## Features Implemented

### UI Recreation

The page layout closely follows the reference design, including:

- Navbar
- Hero banner
- Back button
- Chapter title section
- Verse grid with scroll-style cards
- Footer
- Page background texture

### Interactivity

All visible interactions from the live website were implemented, including:

- Modal open/close
- Sticky modal header
- Tabs (Sanskrit, Transliteration, Translation, Word-by-word, Commentary)
- Word-by-word meaning grid
- Commentary accordion
- Verse navigation arrows
- Audio player
- Scroll-to-top button

### Responsiveness

The layout adapts correctly across mobile, tablet, and desktop screen sizes.

### Technology

Built using the latest stable version of **Svelte + Vite**.

---

## Project Structure

```
project/
│
├── public/
│   ├── gita_banner.png
│   ├── scroll-bg.png
│   └── audio/
│       └── demo.mp3
│
├── src/
│   ├── App.svelte
│   ├── app.css
│   └── pages/
│       └── gita/
│           └── Gita.svelte
│
├── package.json
└── README.md
```

---

## Running the Project Locally

1. Clone the repository

```
git clone <repository-url>
cd <project-folder>
```

2. Install dependencies

```
npm install
```

3. Start development server

```
npm run dev
```

4. Open in browser

```
http://localhost:5173/
```

---

## Deployment Notes

Build the project using:

```
npm run build
```

The generated `dist/` folder can be deployed to Netlify, Vercel, or any static hosting provider.

---

## Next Step: API Integration

The UI and all required interactive elements are complete.
The project is now ready for:

- Fetching chapter and verse data
- Loading Sanskrit text, transliteration, translations
- Loading commentary
- Dynamic audio URLs
- Implementing next/previous verse data updates

Awaiting the provided API details to proceed with integration.

---

End o
