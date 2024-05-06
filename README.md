# WebDevFinal
#### Ale Cuevas
I am creating an outline for a private-facing website, where you can easily edit and view the changes to the public-facing website.

### Website Summary
Below would be a visual summary of the two websites, with some acknowledgement of the backend/database.

#### 1. Homepage:
- **Description**: The homepage serves as the entry point to the website, providing an overview of its content and features.
- **Components**: 
  - Header: Contains navigation links to different sections/pages of the website.
  - Introduction Section: Provides a brief description of the website's purpose and offerings.

#### 2. View All Animals Page:
- **Description**: This page displays a list of animals stored in the database, allowing users to browse through them.
- **Components**:
  - Header/Footer: Navigation links and branding elements.
  - AnimalsList Component: Renders the list of animals fetched from the backend.
  - AnimalItem Component: Displays individual animal entries with details.
  - LoadingSpinner/ErrorMessage Components: Provide feedback during data fetching/error scenarios.
  - Buttons/Links Component: Allows navigation or actions like editing.

#### 3. Add/Edit Animal Page (Private-Facing Website Only):
- **Description**: This page allows users to add new animals to the database or edit existing ones.
- **Components**:
  - Header/Footer: Navigation links and branding elements.
  - AnimalForm Component: Form for adding/editing animal details.
  - SubmitButton Component: Triggers form submission to add it to the database.
  - LoadingSpinner/ErrorMessage Components: Provide feedback during form submission/error scenarios.
  - Buttons/Links Component: Allows navigation back to the "View All Animals" page.

#### 5. Color Picker and Text Style Component (Private-Facing Website Only):
- **Description**: Allows users to customize the website's text style and color scheme.
- **Components**:
  - ColorPicker Component: Provides a UI for selecting colors.
  - 
#### Backend (Python Server):
- **Description**: Implements server-side logic and interacts with the database.
- **Components**:
  - Routes: Define endpoints for handling CRUD operations on animals and color customization.
  - Database Interaction: Interacts with the database to store/retrieve animal data and color settings.
  - Server Setup: Configures the server, sets up routing, middleware, etc.

#### Database:
- **Description**: Stores data related to animals and website settings.
- **Components**:
  - Animal Table: Stores information about each animal, such as name, species, description, etc.
  - Color Settings Table: Stores selected color settings for website customization.

This summary outlines the key components and features of a website that allows users to view, add, and edit animal data, as well as customize the website's color scheme. It covers frontend components, backend functionality, database structure, and additional considerations for a complete web application.


## Components and Hierarchy:

- **App Component**:
  - **Contents**: Entire application.
  - **Children**:
    - Header Component
    - Main Component
    - Footer Component
    - ColorPicker Component

- **ColorPicker Component**:
  - **Contents**: Component for selecting colors.
  - **Children**:
    - ColorSelector Component

- **Header Component**:
  - **Contents**: Top section of the application with links to the other pages.
  - **Children**:
    - Navigation Component

- **Main Component**:
  - **Contents**: Main content area.
  - **Children**:
    - AnimalsList Component (calls to backend for animal data)
    - AnimalForm Component (calls to backend for adding/editing animals)
    - AnimalDetails Component

- **Footer Component**:
  - **Contents**: Bottom section of the application.
  - **Children**:
    - Copyright Component
    - SocialMediaLinks Component

- **Navigation Component**:
  - **Contents**: Navigation menu.
  - **Children**: NavigationLinks Component

- **AnimalsList Component**:
  - **Contents**: Component for displaying a list of animals.
  - **Children**:
    - AnimalItem Component
    - LoadingSpinner Component
    - ErrorMessage Component
  - **Calls to Backend**: Fetches animal data from the backend

- **AnimalForm Component**:
  - **Contents**: Form for adding or editing an animal.
  - **Children**: FormFields Component
  - **Calls to Backend**: Adds/edit animals data to the backend

- **AnimalDetails Component**:
  - **Contents**: Component for displaying details of a specific animal.
  - **Children**: AnimalInfo Component

- **ColorSelector Component**:
  - **Contents**: UI for selecting colors.
  - **Children**: None

- **AnimalItem Component**:
  - **Contents**: Each item in the list of animals.
  - **Children**: None

- **LoadingSpinner Component**:
  - **Contents**: Component to indicate loading state.
  - **Children**: None

- **ErrorMessage Component**:
  - **Contents**: Component to display error messages.
  - **Children**: None

- **FormFields Component**:
  - **Contents**: Fields for entering animal data.
  - **Children**: None

- **AnimalInfo Component**:
  - **Contents**: Display animal details.
  - **Children**: None

- **NavLink Component**:
  - **Contents**: Individual navigation link.
  - **Children**: None

This structure clarifies which components are responsible for interacting with the backend for fetching data or making changes to the database.


# Backend

1. **Routes and Endpoints Definition:**
   - Define routes for handling animal data and user preferences.
   - Distinguish between private (GET, POST, PUT, DELETE) and public (GET) endpoints.

2. **Route Handlers Implementation:**
   - Implement route handlers for CRUD operations on animals and user preferences.
   - Each route handler should include logic for interacting with the database, parsing request bodies, and returning appropriate responses.

3. **Database Interactions:**
   - Connect to the database using a database client library (e.g., Mongoose for MongoDB).
   - Define models or schemas for animals and user preferences to structure data in the database.
   - Implement functions for CRUD operations on animals and user preferences, utilizing database queries and operations provided by the database client library.

4. **Middleware and Error Handling:**
   - Set up middleware functions to handle common tasks such as request parsing, CORS (Cross-Origin Resource Sharing), and logging.
   - Implement error handling middleware to catch and handle errors gracefully, providing meaningful error messages in responses.

5. **Server Configuration:**
   - Initialize the server framework (e.g., Express.js) and configure it to handle HTTP requests.
   - Associate route handlers with their corresponding endpoints.
   - Start the server to listen for incoming requests on a specific port.

### More Backend Details:

1. **CRUD Operations Functions:**
   - Define functions for CRUD operations on the database:
     - `retrieveData(query)`: Query the database to fetch data based on the provided criteria.
     - `addData(data)`: Insert new data into the appropriate database table or collection.
     - `updateData(id, newData)`: Update an existing record in the database with the new data.
     - `deleteData(id)`: Delete a record from the database based on its identifier.

2. **Route Handlers Definition:**
   - Define routes and corresponding handlers for CRUD operations:
     - `GET /animals`: Handler to retrieve all animals from the database.
     - `POST /animals`: Handler to add a new animal to the database.
     - `GET /animals/:id`: Handler to retrieve a specific animal by its ID.
     - `PUT /animals/:id`: Handler to update an existing animal by its ID.
     - `DELETE /animals/:id`: Handler to delete an animal by its ID.
     - `GET /preferences`: Handler to retrieve user preferences for text size and stylization.
     - `POST /preferences`: Handler to update user preferences for text size and stylization.

### Additional Considerations:
- **Authentication/Authorization**: User authentication state may be shared between components to control access to certain pages or actions.
- **Form Validation**: Error messages or validation state may be shared between components to handle form input validation.
- **Loading/Error Handling**: Loading and error states may be shared between components to provide feedback to users during data fetching or form submission operations.


# How the Color Change Component would work

The color change selector component (as well as what will control the other stylistic changes) will be present only in the private editing website. The public-facing website will recieve the information about the chosen colors and styles from the shared database.

1. **Parent Component**:
   - Maintain the selected color state in the parent component.
   - Pass the selected color as a prop to each child component.
   - Provide a callback function in the parent component to handle color changes.

2. **Child Components**:
   - Receive the selected color as a prop.
   - Use the received color prop to apply styles or other attributes dynamically.

Here's an example implementation:

```jsx
// ParentComponent.js

import React, { useState } from 'react';
import ColorPicker from './ColorPicker';
import Component1 from './Component1';

import Component2 from './Component2';

const ParentComponent = () => {
    const [selectedColor, setSelectedColor] = useState('#000000'); // Default color

    const handleColorChange = (color) => {
        setSelectedColor(color); // Update selected color
    };

    return (
        <div>
            <ColorPicker defaultColor={selectedColor} onColorChange={handleColorChange} />
            <Component1 color={selectedColor} />
            <Component2 color={selectedColor} />
        </div>
    );
};

export default ParentComponent;
```

This would be an example where the child component's background color is changed
```jsx
// Component1.js

import React from 'react';

const Component1 = ({ color }) => {
    return (
        <div style={{ backgroundColor: color }}>
            <h2>Component 1</h2>
            <p>This component changes its background color based on the selected color.</p>
        </div>
    );
};

export default Component1;
```

This is an example where the child component's text color is changed.
```jsx
// Component2.js

import React from 'react';

const Component2 = ({ color }) => {
    return (
        <div style={{ color: color }}>
            <h2>Component 2</h2>
            <p>This component changes its text color based on the selected color.</p>
        </div>
    );
};

export default Component2;
```

In this example:

- The `ParentComponent` manages the `selectedColor` state and passes it down to `Component1` and `Component2` as props.
- Whenever the color changes, the `handleColorChange` function updates the `selectedColor` state in the parent component.
- The `color` prop received by `Component1` and `Component2` is used to dynamically apply styles.

This way, a change in the color picker component in the parent component will automatically propagate down to all child components, updating their appearance accordingly.
In addition, 

A similar logic will be applied for the other stylistic choices that the user will be able to modify in the private editing website.






