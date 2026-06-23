#  YelpCamp

A full-stack campground review platform where users can explore campgrounds, write reviews, give star ratings, and upload photos. Built with Node.js, Express, MongoDB, and an NLP-powered sentiment analysis pipeline that automatically classifies reviews and generates personalized recommendations.

---

## Features

- **User Authentication** — Register, login, and logout with Passport.js (local strategy + session management)
- **Campground CRUD** — Create, view, edit, and delete campgrounds with image uploads via Cloudinary
- **Review System** — Post reviews with star ratings; reviews are tied to authenticated users
- **NLP Sentiment Analysis** — Every review is automatically analyzed using the `sentiment` and `@xenova/transformers` libraries to classify tone and surface better campground recommendations
- **Flash Messages** — User-friendly success/error feedback on all actions
- **Input Validation** — Server-side validation using Joi schemas on all forms
- **Responsive UI** — EJS-rendered templates with CSS styling

---

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Framework | Express.js |
| Templating | EJS + EJS-Mate (layouts) |
| Database | MongoDB + Mongoose |
| Auth | Passport.js, passport-local, passport-local-mongoose |
| File Uploads | Multer + Cloudinary (multer-storage-cloudinary) |
| NLP | `sentiment` v5, `@xenova/transformers` v2 |
| Validation | Joi |
| Sessions | express-session + connect-flash |
| Dev Tools | dotenv, method-override |

---

## Project Structure

```
YelpCamp/
├── controller/        # Route handler logic (campgrounds, reviews, users)
├── model/             # Mongoose schemas (Campground, Review, User)
├── routes/            # Express routers
├── views/             # EJS templates
│   └── campgrounds/   # Index, show, new, edit pages
├── public/            # Static assets (CSS, client JS)
├── seeds/             # Database seeding scripts
├── utils/             # Helpers (async error wrapper, AppError class)
├── cloud.js           # Cloudinary + Multer config
├── errorSchema.js     # Joi validation schemas
├── rec.js             # NLP recommendation engine
└── index.js           # App entry point
```

---

## Getting Started

### Prerequisites

- Node.js v18+
- MongoDB (local or Atlas)
- A Cloudinary account (for image uploads)

### Installation

```bash
# Clone the repo
git clone https://github.com/vaibhavj2006/Yelpcamp.git
cd Yelpcamp

# Install dependencies
npm install
```

### Environment Variables

Create a `.env` file in the root directory:

```env
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_KEY=your_api_key
CLOUDINARY_SECRET=your_api_secret
SESSION_SECRET=your_session_secret
DB_URL=mongodb://localhost:27017/yelpcamp
```

### Seed the Database (optional)

```bash
node seeds/index.js
```

### Run the App

```bash
node index.js
```

Visit `http://localhost:3000` in your browser.

---

## How the NLP Pipeline Works

Every review submitted by a user is passed through two layers of analysis:

1. **Sentiment scoring** (`sentiment` library) — assigns a numeric score based on positive/negative word weights in the review text.
2. **Transformer-based classification** (`@xenova/transformers`) — runs a lightweight transformer model in-process to classify review sentiment with higher accuracy.

The results are stored alongside the review and used to rank campgrounds — campgrounds with consistently positive sentiment scores surface higher in recommendations.

---



## Author

**Vaibhav Joshi**
[GitHub](https://github.com/vaibhavj2006) 
