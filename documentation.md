# AO3 Website Documentation

## Table of Contents
- [Overview](#overview)
- [Getting Started](#getting-started)
- [Architecture](#architecture)
- [Features](#features)
- [Components](#components)
- [API Integration](#api-integration)
- [Extension Integration](#extension-integration)
- [State Management](#state-management)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)

## Overview

The AO3 Website is a companion web application for the AO3 Chrome Extension. It provides user authentication, dashboard functionality, and reading list management for Archive of Our Own (AO3) users. The website works in tandem with the Chrome extension to enhance the AO3 reading experience.

### Tech Stack
- Frontend: React + Vite
- Styling: Tailwind CSS
- Animation: Framer Motion
- Routing: React Router DOM
- HTTP Client: Axios
- UI Components: HeadlessUI, Lucide React

## Getting Started

### Prerequisites
- Node.js 16.x or higher
- npm 7.x or higher
- Git

### Installation

1. Clone the repository:
```bash
git clone https://github.com/GDGVIT/ao3-chrome-extension-frontend.git
```

2. Install dependencies:
```bash
cd ao3-chrome-extension-frontend
npm install
```

3. Create environment variables:
```env
VITE_API_URL=your_api_url
VITE_EXTENSION_ID=your_extension_id
```

4. Start development server:
```bash
npm run dev
```

## Architecture

The application follows a component-based architecture using React and implements the following structure:

```
src/
├── components/         # Reusable UI components
├── pages/             # Page components
├── hooks/             # Custom React hooks
├── services/          # API services
├── utils/             # Utility functions
├── contexts/          # React contexts
└── assets/           # Static assets
```

## Features

### 1. Authentication
- Login with username/password
- Sign up new account
- Token-based authentication
- Password recovery

### 2. Dashboard
- Reading history
- Bookmarked works
- Recent activity
- Tag management

### 3. Notes Management
- Create/edit/delete notes
- Tag-based organization
- Search functionality
- Completion status tracking

### 4. Bookmarks
- Save bookmarks
- Tag bookmarks
- Filter by tags
- Search functionality

### 5. Settings
- Update username
- Manage preferences
- Extension integration settings

## Components

### Core Components

#### Sidebar (`components/Sidebar/Sidebar.tsx`)
Main navigation component with links to:
- Dashboard
- Notes
- Bookmarks
- History
- Settings

#### Authentication Forms
- Login form
- Sign up form
- Password recovery form

### Page Components

#### Notes Page (`pages/Notes/Notes.tsx`)
Features:
- Note creation modal
- Tag management
- Search and filtering
- Completion tracking

#### Bookmarks Page (`pages/Bookmarks/Bookmarks.tsx`)
Features:
- Tag-based filtering
- Search functionality
- Fandom categorization
- Sort by date

#### History Page (`pages/History/History.tsx`)
Features:
- Reading history list
- Date-based organization
- Tag filtering
- Search capability

## API Integration

### Authentication Endpoints

```typescript
// Login
POST /auth/login
Body: { username: string, password: string }
Response: { accessToken: string, refreshToken: string }

// Sign Up
POST /auth/signup
Body: { username: string, password: string, email: string }
Response: { success: boolean, message: string }

// Update Username
PATCH /auth/update_username
Body: { new_username: string }
Headers: { Tokens: { accessToken: string, refreshToken: string } }
Response: { success: boolean, message: string }
```

### Data Endpoints

```typescript
// Get User Details
GET /auth/userdetail
Headers: { Tokens: { accessToken: string, refreshToken: string } }
Response: { username: string, ... }

// Get Recommendations
GET /recommendations/:username
Response: { [tag: string]: string[] }
```

## Extension Integration

### Token Exchange
1. Website generates authentication tokens
2. Tokens are securely passed to extension
3. Extension uses tokens for API requests

### Communication Flow
1. User authenticates on website
2. Website stores tokens in localStorage
3. Extension retrieves tokens when needed
4. Both maintain synchronized state

## State Management

The application uses React's Context API for state management:

```typescript
// Auth Context
const AuthContext = createContext({
  isAuthenticated: false,
  user: null,
  login: (tokens) => {},
  logout: () => {},
});

// Notes Context
const NotesContext = createContext({
  notes: [],
  addNote: (note) => {},
  deleteNote: (id) => {},
  updateNote: (id, note) => {},
});
```

## Deployment

### Build Process

1. Create production build:
```bash
npm run build
```

2. Preview build:
```bash
npm run preview
```

### Deployment Checklist
- [ ] Environment variables configured
- [ ] API endpoints updated
- [ ] Extension ID verified
- [ ] Build successful
- [ ] Assets optimized

## Troubleshooting

### Common Issues

1. **Authentication Errors**
   - Check token expiration
   - Verify API endpoint URLs
   - Clear localStorage and retry

2. **Extension Communication Issues**
   - Verify extension ID
   - Check message passing implementation
   - Confirm extension permissions

3. **API Connection Issues**
   - Verify API status
   - Check CORS configuration
   - Validate request headers

### Debug Mode

Enable debug mode by setting:
```typescript
localStorage.setItem('debug', 'true');
```

This will enable detailed console logging for:
- API requests
- Extension communication
- State changes
- Authentication flow

## Support

For additional support:
- Create an issue on GitHub
- Join our Discord server
- Contact GDSC-VIT team

---

This documentation is maintained by GDSC-VIT and will be updated as the project evolves.