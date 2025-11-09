# CarbonSense 2.0 - Smart Sustainability Companion

## Overview
CarbonSense 2.0 is an AI-powered sustainability companion that helps users understand, track, and reduce their carbon footprint through personalized insights, real-time tracking, and smart recommendations.

## Features

### 1. User Profile System
- Personalized user profiles with sustainability preferences
- Transport type tracking (car, EV, bike, public transport, walk)
- Home energy usage levels (low, medium, high)
- Location-based recommendations
- Badge system (Bronze/Silver/Gold Eco Hero)
- EcoPoints gamification

### 2. Carbon Footprint Dashboard
- Real-time tracking of:
  - Energy usage (kWh)
  - Water consumption (L)
  - Travel distance (km)
  - CO₂ emissions (kg)
- Carbon calculator with multiple inputs
- Interactive charts showing trends over time
- Activity timeline with recent eco-actions
- CO₂ calculation multipliers for different transport types

### 3. Smart Eco-Route Mapping
- Live GPS tracking using browser Geolocation API
- **OpenRouteService API integration** for real turn-by-turn navigation
  - Geocoding addresses to coordinates
  - Route calculation for car, bike, and walk modes
  - Elevation-based CO₂ calculations for accuracy
  - 1-hour route caching to optimize API usage
  - Partial result handling (preserves successful routes if one mode fails)
- Route comparison (default vs eco-friendly) with real distance/duration data
- Real-time CO₂ savings calculations based on actual routes
- Points rewards for choosing eco-friendly routes (+15 EcoPoints)
- **Future enhancement**: Interactive map visualization with polylines (currently shows route data in cards)

### 4. AI Sustainability Advisor
- OpenAI GPT-5 powered chatbot (with fallback system)
- Personalized eco-tips based on user profile
- Context-aware recommendations
- Product and action suggestions
- **Robust fallback mode** with pre-written eco-tips when OpenAI unavailable
- Chat history persistence in localStorage
- Fixed: apiRequest now properly parses JSON responses
- Fixed: State management uses functional updates to prevent stale state issues

### 5. Dynamic Features
- Dynamic backgrounds that change based on carbon footprint level
  - Green gradient for low emissions
  - Yellow-green for medium emissions
  - Orange gradient for high emissions
- Smooth Framer Motion animations throughout
- Responsive design for mobile and desktop
- Beautiful loading and error states

## Tech Stack

### Frontend
- React 18 with Vite
- TypeScript
- Tailwind CSS
- Framer Motion for animations
- Recharts for data visualization
- Lucide React for icons
- Wouter for routing
- TanStack Query for data fetching
- shadcn/ui components

### Backend
- Express.js
- OpenAI API (GPT-5)
- LocalStorage for data persistence (MVP)
- TypeScript

### Design System
- Poppins font for headings
- Inter font for body text
- Green color palette (primary: #16a34a)
- Consistent spacing and typography
- Dark mode support

## Data Models

### UserProfile
- id, name, location
- transport, energyUse
- ecoPoints, level
- createdAt

### CarbonStats
- id, userId
- energy, water, travel, emissions
- timestamp

### Activity
- id, userId, type
- description, points
- timestamp

### Route
- origin, destination
- distance, duration, co2Emissions
- type, transportMode

## API Endpoints

### POST /api/chat
- Handles AI sustainability advice requests
- Accepts user message and profile context
- Returns AI response and personalized eco-tips
- Fallback mode if OpenAI is unavailable

### POST /api/routes/compare
- Compares default (car) vs eco (bike) routes
- Request: { origin: string, destination: string }
- Response: { default: Route | null, eco: Route | null, partial: boolean }
- Uses OpenRouteService for real routing data
- Includes route caching and partial result handling
- Returns fallback flag if both routes fail

## Data Persistence
- LocalStorage used for MVP implementation
- User profiles stored locally
- Carbon stats tracked over time
- Activity history maintained
- Chat messages saved

## CO₂ Calculation Multipliers
- Car: 0.21 kg/km
- EV: 0.05 kg/km
- Public transport: 0.089 kg/km
- Bike: 0 kg/km
- Walk: 0 kg/km
- Energy: 0.5 kg/kWh
- Waste: 0.3 kg/kg

## EcoPoints & Levels
- Calculator use: +5 points
- Eco-route selection: +15 points
- Following AI tip: +5 points
- Profile completion: +10 points

### Levels
- Bronze: 0-99 points
- Silver: 100-299 points
- Gold: 300+ points

## Key Features for Users

1. **Profile Setup**: Create a profile to receive personalized recommendations
2. **Track Impact**: Monitor daily carbon footprint across multiple categories
3. **Get AI Advice**: Chat with AI for eco-friendly tips and product recommendations
4. **Compare Routes**: See CO₂ savings from choosing eco-friendly transportation
5. **Earn Rewards**: Collect EcoPoints and level up through sustainable actions
6. **Visual Feedback**: Dynamic backgrounds reflect your environmental performance

## Development

### Running the App
```bash
npm run dev
```

### Environment Variables
- `OPENAI_API_KEY`: Required for AI advisor functionality
- `SESSION_SECRET`: Auto-generated for session management

## Future Enhancements
- Google Maps JavaScript API integration for real route mapping
- Backend database persistence (PostgreSQL)
- Social sharing features
- Community leaderboards
- Real-time carbon offset recommendations
- Firebase Auth for multi-device sync
- Advanced analytics and goal tracking

## User Journey

1. **Onboarding**: User creates profile with basic sustainability preferences
2. **Dashboard**: View current carbon footprint and use calculator
3. **AI Advisor**: Get personalized eco-tips and product recommendations
4. **Route Planning**: Compare routes and choose eco-friendly options
5. **Progress**: Earn points, level up badges, and track improvements over time

## Notes
- The app uses localStorage for MVP data persistence
- Maps feature uses mock data with fallback capability
- AI advisor works with OpenAI GPT-5 or falls back to local recommendations
- GPS tracking requires browser geolocation permission
- Designed mobile-first with responsive layouts throughout
