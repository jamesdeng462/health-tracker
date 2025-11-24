Kakuma Health Tracker ‚Äî README

The Kakuma Health Tracker is a web-based application designed to monitor, visualize, and analyze malaria and water-borne disease cases across various zones within Kakuma.
The platform retrieves data directly from Firebase Firestore, allowing health workers, NGOs, researchers, and community officials to track public health trends in real time.

Ì≥å Project Purpose

The main goal of this application is to offer a simple, fast, and accessible way to understand disease distribution across the Kakuma region.
It helps users:

Identify high-risk zones quickly

Compare disease counts between areas

Support health-related planning and interventions

Visualize trends using interactive charts

This project is especially valuable in humanitarian and public-health environments where accurate data is essential for decision-making.

Ì≥Ç Features
Ì¥ç 1. Search Functionality

Users can search for any zone by name. The UI updates dynamically to show only relevant results.

Ì¥É 2. Sorting System

Sort data by:

Malaria cases

Water-borne disease cases

Supports ascending and descending order toggling.

Ì≥ä 3. Interactive Chart Visualization (Chart.js)

The application uses Chart.js to render a bar chart that displays:

Malaria cases per zone

Water-borne disease cases per zone

The chart updates automatically when the user:

Searches

Sorts

Filters the data

Ì≥Å 4. Dynamic Firebase Integration

Real-time data is fetched from Firebase Firestore, ensuring that the numbers displayed always match the database.

Ì≤° 5. Summary Statistics

At a glance, users can see:

Total malaria cases

Total water-borne cases

Ì∂• 6. Clean & Modern User Interface

Built with simple HTML and CSS, the interface is:

Mobile-friendly

Easy to navigate

Clean and visually appealing

Ì∑© Technologies Used
Area	Technology
Frontend	HTML5, CSS3, JavaScript
Backend / API	Firebase Firestore
Chart Visualization	Chart.js
Hosting	Any static web server or Firebase Hosting
