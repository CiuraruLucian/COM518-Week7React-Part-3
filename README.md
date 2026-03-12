# React Context, Maps, and API Search Exercises

This repository contains a set of React exercises completed in class to explore component state management, the React Context API, asynchronous data fetching, and integrating interactive maps.

The exercises demonstrate how to pass data through a component hierarchy, replace prop drilling with context, perform API-based searches, and visualize location data using a map.

---

## Overview

The project builds a small React application that allows users to:

- Search for locations using an API
- Display search results as a list
- Show locations on an interactive map
- Toggle between light and dark mode
- Share state between components using React Context

The exercises progress from basic prop-based state passing to a more scalable architecture using Context and reusable components.

---

## Learning Objectives

This project demonstrates the following React concepts:

- Component hierarchy and prop passing
- React Context API
- State lifting
- React Hooks (`useState`, `useEffect`, `useContext`)
- Asynchronous API requests using `fetch`
- Component modularisation
- Map integration with Leaflet

---

## Exercise 1 – Prop Drilling

Initially, the application demonstrates **prop drilling**, where state is passed through multiple components via props.

### Component Structure

```
App
├── Search
│   └── SearchResults
└── ModeChooser
```

The `App` component stores the dark/light mode state and passes it down to child components through props.

While this works for small applications, it can become difficult to maintain when many components require access to the same state.

---

## Using React Context

To improve scalability, the dark mode state is moved into a **React Context**.

### Steps

1. Create a context file:

```
darkmodecontext.ts
```

2. Provide the context in the top-level component:

```jsx
<DarkModeContext.Provider value={mode === "dark"}>
    <Search />
</DarkModeContext.Provider>
```

3. Access the context in child components:

```jsx
const darkMode = useContext(DarkModeContext);
```

This allows nested components to access shared state directly without passing props through intermediate components.

---

## Multiple Contexts

The exercises also demonstrate using multiple contexts at the same time.

Example contexts include:

- `NameContext`
- `CourseContext`

Providers can be nested so that multiple pieces of shared state can be accessed by child components.

---

## Map Component

The Leaflet map is separated into its own component to improve modularity.

### Responsibilities

- Receive `latitude` and `longitude` as props
- Initialize the map when the component loads
- Display markers for search results

Example structure:

```
App
├── MapComponent
└── SearchComponent
```

---

## Place Search API

The application performs a location search using the following API:

```
https://hikar.org/webapp/nomproxy?q=PLACE_NAME
```

This service returns OpenStreetMap location data.

### Features

- Input form for entering a place name
- Asynchronous search using `fetch`
- Results stored in state
- Dynamic rendering of results as JSX

---

## Lifting State

Search results are lifted to the main `App` component so they can be shared between:

- The results list
- The map markers

This ensures there is a **single source of truth** for the search data.

---

## Dark Mode

Dark mode is implemented using React Context so that any component can access the theme state and update its styles accordingly.

---

## Advanced Feature

Each search result includes a button labelled:

```
Go to this location
```

When clicked:

- The map updates its latitude and longitude
- The map centers on the selected location
- A marker appears on the map

---

## Technologies Used

- React
- TypeScript
- React Hooks
- Leaflet
- OpenStreetMap / Nominatim API
- Fetch API

---

## Example Project Structure

```
src
 ├── components
 │   ├── MapComponent.tsx
 │   ├── SearchComponent.tsx
 │   ├── SearchResults.tsx
 │   └── ModeChooser.tsx
 │
 ├── context
 │   └── DarkModeContext.ts
 │
 ├── App.tsx
 └── main.tsx
```

---

## Author

Created as part of a React classroom exercise to practice state management, context usage, and integrating external APIs.
