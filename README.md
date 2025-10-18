# 🍜 BostonNoms — Interactive Restaurant Discovery

**Developers:** Nicole Lin & Jolly Zheng  
**Date:** March 2025  

---

## Overview

BostonNoms is an interactive data visualization web app built with **Leaflet.js**, **D3.js**, and **JavaScript**, designed to help users explore Boston restaurants through a data-driven and intuitive interface.

BostonNoms empowers users to:

- Choose where they want to search (via a draggable person icon),
- Compare restaurants by distance and rating reliability,
- Filter by cuisine type, and
- Visually connect spatial and statistical insights through an interactive map-scatterplot system.

---

## How to Use

1. **Drag the Person Icon**  
   - Move the icon anywhere on the Boston map to set your desired location.  
   - Coordinates will appear, and the scatterplot automatically recalculates distance metrics.

2. **Explore the Scatterplot**  
   - Each point represents a restaurant.  
   - Brush (click and drag) to highlight restaurants within your preferred **distance** and **rating range**.  
   - The selected restaurants will glow in red on the map.

3. **Click Map Markers**  
   - Hover to see restaurant name and raw rating.  
   - Click to view details, including address, categories, and review snippet.

4. **Filter by Cuisine**  
   - Use the filter buttons under the map to select categories like “Dessert,” “Seafood,” or “Bar.”  
   - Click **Clear** to reset filters.

5. **Compare and Decide!**  
   - Use the combination of map and scatterplot to balance **distance vs. reliability**, identifying ideal restaurants near your chosen spot.

---

## Dataset

The project uses the `yelp_boston.csv` dataset, containing:

| Field | Description |
|--------|--------------|
| `name` | Restaurant name |
| `url` | Yelp listing link |
| `review_count` | Number of Yelp reviews |
| `rating` | Average Yelp rating |
| `categories_json` | JSON list of categories |
| `snippet_text` | A short excerpt from a user review |
| `latitude`, `longitude` | Geographic coordinates |
| `neighborhood`, `city`, `postal_code` | Location metadata |

The audience is users who want to **find hangout spots** based on proximity, cuisine, and review quality.

---

## Key Features

### Interactive Map (Leaflet.js + Mapbox API)

- Zoomable and pannable map of Boston.
- Each restaurant shown as a colored circle marker.
- Hover: displays restaurant name + raw star rating.
- Click: opens an information box with address, tags, and review snippet.
- Map dynamically highlights restaurants selected in the scatterplot.

### Drag-and-Drop Personalization

- A draggable **“person” icon** lets users drop their location anywhere on the map.  
- The scatterplot automatically updates distances and recalculates restaurant rankings relative to that location.  
- Coordinates (latitude & longitude) are displayed after dropping the icon.

### Interactive Scatterplot (D3.js)

- **X-axis:** distance from dropped location (in miles)  
- **Y-axis:** *normalized rating score* (via **Bayesian Average**)  
- **Brush tool:** lets users select ranges of distance and score; linked points on the map highlight in red.  
- **Color legend:** communicates rating confidence visually.

**Bayesian normalization formula** smooths out biases from restaurants with few reviews:  
\[
\text{Weighted Rating} = \frac{v}{v+k}R + \frac{k}{v+k}C
\]
where

- *v* = number of reviews  
- *R* = restaurant’s average rating  
- *C* = assumed baseline rating (3.0 in this project)  
- *k* = prior weight (set to 3)

This method stabilizes ratings and avoids overvaluing new or low-review restaurants.

### Filter System

- Filter buttons let users view only specific cuisines or business categories (e.g., “Cafes,” “Italian,” “Asian Fusion”).  
- A **Clear** button resets all filters for a fresh search.

### Visual Cohesion

- Dynamic brushing between map and scatterplot creates a **bidirectional link** between spatial and quantitative data.  
- Hover tooltips and chat-bubble-style review snippets provide clear and enjoyable feedback.

---

## Tech Stack

| Component | Technology |
|------------|-------------|
| **Frontend** | HTML, CSS, JavaScript |
| **Visualization** | D3.js (scatterplot, brushing), Leaflet.js (map), Mapbox API |
| **Data Processing** | JavaScript + D3 data joins |
| **Computation** | Bayesian Average for normalized ratings |
| **Design** | “Cool light” aesthetic for readability and modern look |

---

## Development Challenges & Trade-offs

- **Drag vs. Map Panning:** Implementing draggable icons conflicted with Leaflet’s built-in map drag. Solved by prioritizing icon placement before map movement.  
- **Pin Accuracy:** Slight offsets occur when dropping the icon due to image size, but impact is minimal.  
- **Cluster Overlap:** Raw ratings led to tight point clustering; Bayesian normalization improved data distribution and readability.  
- **Balance Between Accuracy & Discovery:** Normalization improved fairness but reduced exposure for new restaurants — mitigated by color-coding unnormalized ratings.

---

## Development Roles

**Nicole Lin**

- Map + Leaflet + Mapbox API integration  
- Tooltip + star-rating visuals  
- HTML/CSS layout and animations  
- D3 scatterplot design + brush tool linkage  
- Filter system and button styling  
- UI/UX refinement and documentation  

**Jolly Zheng**

- Scatterplot logic and Bayesian normalization  
- Legend and rating computations  
- Dataset preprocessing  
- Co-design of interactions and debugging