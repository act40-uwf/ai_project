# AI Meal Planner - Sprint 1 MVP

A JavaScript-based web application for meal planning, pantry management, and grocery list generation. This is the first iteration of a 4-sprint development cycle focused on establishing foundational architecture and core functionality.

## Features

### ✅ Sprint 1 Feature Checklist

- [x] **Pantry Inventory System**
  - Add ingredients with quantities and units
  - View current pantry items
  - Remove pantry items
  - Automatic quantity aggregation for duplicate ingredients

- [x] **Recipe Database Interface**
  - Browse 30 sample recipes with complete data
  - Search recipes by name or ingredient
  - Filter recipes by difficulty level (Easy, Medium, Hard)
  - Filter recipes that use pantry items (prioritized by match ratio)
  - View detailed recipe information in modal

- [x] **AI-Powered Recipe Recommendation Engine**
  - Recipe prioritization based on pantry inventory
  - Match scoring based on ingredient overlap
  - Recipes sorted by pantry utilization ratio

- [x] **Weekly Meal Planning Interface**
  - 7-day meal plan view (Monday through Sunday)
  - Three meals per day (Breakfast, Lunch, Dinner)
  - Week navigation (previous/next week)
  - Recipe selection dropdowns for each meal slot
  - Persistent meal plan storage

- [x] **Automatic Grocery List Generator**
  - Generates shopping list from meal plan
  - Subtracts pantry inventory from recipe requirements
  - Unit conversion for ingredient matching
  - Groups items by ingredient name
  - Displays quantities needed

- [x] **Nutrition Tracking Component**
  - Weekly nutrition summary (total calories, protein, carbs, fats)
  - Daily nutrition breakdown
  - Per-serving nutritional information
  - Automatic calculation based on meal plan

## Setup Instructions

### Prerequisites

- Modern web browser (Chrome, Firefox, Safari, Edge)
- No server or backend required - runs entirely client-side

### Installation

1. Clone or download this repository
2. Ensure all files are in the same directory:
   - `index.html`
   - `styles.css`
   - `app.js`
   - `README.md`

### Running the Application

1. Open `index.html` in your web browser
   - You can double-click the file, or
   - Right-click and select "Open with" → your preferred browser
   - Or use a local web server (optional):
     ```bash
     # Using Python 3
     python -m http.server 8000
     
     # Using Node.js (with http-server)
     npx http-server
     ```
     Then navigate to `http://localhost:8000`

2. The application will load with:
   - 30 sample recipes pre-loaded
   - Empty pantry (ready for input)
   - Empty meal plan (ready for selection)
   - All data persisted in browser localStorage

### Deploying to GitHub Pages

This application can be deployed as a static site using GitHub Pages:

1. Go to your repository on GitHub: https://github.com/act40-uwf/ai_project
2. Click **Settings** (top right of repository)
3. In the left sidebar, click **Pages**
4. Under **Source**, select:
   - Branch: `main`
   - Folder: `/ (root)`
5. Click **Save**

Your application will be live at:
**https://act40-uwf.github.io/ai_project/**

> Note: It may take a few minutes for the site to be available after enabling GitHub Pages. You can check the deployment status in the **Actions** tab of your repository.

## Usage Guide

### Managing Your Pantry

1. Navigate to the **Pantry** tab
2. Enter an ingredient name (e.g., "chicken breast")
3. Enter the quantity and select a unit
4. Click "Add to Pantry"
5. View all pantry items below
6. Remove items using the "Remove" button

### Browsing Recipes

1. Navigate to the **Recipes** tab
2. Use the search bar to find recipes by name or ingredient
3. Filter by difficulty using the dropdown
4. Click "Show Recipes Using Pantry Items" to see recommendations
5. Click on any recipe card to view full details

### Planning Meals

1. Navigate to the **Meal Plan** tab
2. Use the week navigation buttons to select a week
3. For each day and meal, select a recipe from the dropdown
4. Your selections are automatically saved
5. Navigate between weeks to plan ahead

### Generating Grocery Lists

1. First, create a meal plan (see above)
2. Navigate to the **Grocery List** tab
3. Click "Generate Grocery List"
4. The list shows items needed, minus what's in your pantry
5. Items are grouped by ingredient name

### Tracking Nutrition

1. Navigate to the **Nutrition** tab
2. View weekly totals for calories, protein, carbs, and fats
3. Scroll down to see daily breakdowns
4. Nutrition updates automatically as you modify your meal plan

## Technical Architecture

### Data Structures

**Recipe Object:**
```javascript
{
  id: number,
  name: string,
  ingredients: [{ name: string, quantity: number, unit: string }],
  instructions: [string],
  servings: number,
  nutrition: { calories: number, protein: number, carbs: number, fats: number },
  prepTime: number,
  difficulty: "Easy" | "Medium" | "Hard"
}
```

**Pantry Item:**
```javascript
{
  name: string,
  quantity: number,
  unit: string
}
```

**Meal Plan:**
```javascript
{
  "monday_breakfast": recipeId,
  "monday_lunch": recipeId,
  // ... etc
}
```

### Key Algorithms

1. **Recipe-Pantry Matching**: Normalizes ingredient names and performs fuzzy matching to identify pantry items that can be used in recipes.

2. **Grocery List Generation**: 
   - Aggregates all ingredients from selected meals
   - Matches ingredients with pantry items
   - Performs unit conversions where possible
   - Subtracts pantry quantities from recipe requirements

3. **Nutrition Calculation**: Sums nutritional values from all selected recipes, assuming 1 serving per meal.

### Data Persistence

All application state is saved to browser `localStorage`:
- Pantry items
- Meal plan selections
- Current week view

Data persists across browser sessions and page refreshes.

## Sample Recipe Dataset

The application includes 30 diverse recipes covering:
- Breakfast items (pancakes, omelette, French toast, avocado toast)
- Main dishes (chicken, beef, fish, vegetarian options)
- Salads and sides (Greek salad, Caesar salad, Caprese salad)
- Pasta dishes (carbonara, primavera, lasagna)
- International cuisine (curry, teriyaki, fajitas, tacos)
- Desserts (chocolate chip cookies)

Each recipe includes:
- Complete ingredient lists with quantities and units
- Step-by-step instructions
- Nutritional information per serving
- Preparation time
- Difficulty rating

## Known Limitations (Sprint 1)

### Ingredient Matching
- Unit conversion is simplified and may not handle all cases
- Ingredient name matching uses basic string comparison (exact or substring)
- No handling for ingredient synonyms (e.g., "tomato" vs "tomatoes")
- No support for ingredient substitutions

### Grocery List Generation
- Assumes 1 serving per meal (no portion size adjustment)
- Unit conversions are limited to common conversions
- No categorization of grocery items (produce, meat, dairy, etc.)
- No handling for recipe scaling

### Nutrition Tracking
- Fixed to 1 serving per meal (no portion size adjustments)
- No daily calorie goals or limits
- No macro ratio calculations
- No micronutrient tracking

### Recipe Database
- Static dataset (no dynamic recipe addition)
- No recipe editing or customization
- No user recipe uploads
- No recipe ratings or reviews

### Meal Planning
- No meal prep scheduling
- No recipe scaling for multiple servings
- No dietary restriction filtering
- No meal type preferences (vegetarian, vegan, etc.)

### User Experience
- No user accounts or multi-user support
- No data export/import
- No print functionality for grocery lists
- No mobile-optimized layout (responsive but basic)

## Notes for Sprint 2 Improvements

### Priority Enhancements

1. **Enhanced Ingredient Matching**
   - Implement comprehensive unit conversion library
   - Add ingredient synonym database
   - Improve fuzzy matching algorithm
   - Support for ingredient substitutions

2. **Portion Size Adjustments**
   - Allow users to specify servings per meal
   - Scale nutrition calculations accordingly
   - Update grocery list quantities based on portions

3. **Recipe Customization**
   - Allow users to add custom recipes
   - Edit existing recipes
   - Save favorite recipes
   - Recipe scaling functionality

4. **Improved Grocery List**
   - Categorize items (produce, meat, dairy, pantry, etc.)
   - Add checkboxes for shopping
   - Print-friendly format
   - Export to shopping apps

5. **Enhanced Nutrition Features**
   - Daily calorie goals
   - Macro ratio tracking
   - Micronutrient information
   - Nutrition charts and graphs

6. **Dietary Restrictions**
   - Filter recipes by dietary preferences
   - Allergen tracking
   - Vegetarian/vegan/gluten-free filters

7. **AI Integration Preparation**
   - Structure data for AI model training
   - User feedback collection mechanism
   - Recipe recommendation scoring system
   - Data export for model training

### Technical Debt

- Refactor unit conversion into separate utility module
- Implement more robust ingredient matching service
- Add input validation and error handling
- Improve code modularity for easier testing
- Add unit tests for core algorithms

### Research Questions Preparation

For Sprint 3 A/B testing:
- Implement user feedback tracking
- Add analytics for feature usage
- Structure data collection for model training
- Prepare baseline metrics for comparison

## Browser Compatibility

Tested and working on:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

Requires JavaScript enabled. Uses modern ES6+ features.

## File Structure

```
course project/
├── index.html      # Main HTML structure
├── styles.css      # Application styling
├── app.js          # Core application logic
└── README.md       # This file
```

## License

This project is part of an academic research project. All code is provided for educational and research purposes.

## Contact

For questions or issues related to this Sprint 1 MVP, please refer to the project documentation or contact the development team.

---

**Sprint 1 Status**: ✅ Complete - All core features implemented and functional

