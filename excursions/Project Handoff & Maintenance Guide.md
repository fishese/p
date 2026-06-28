# **Cruise Strategy Dashboard \- Maintenance & Handoff Guide**

This document explains how the itinerary\_planner.html file works and how to safely update the information inside it as your travel date (May 2027\) approaches.

## **1\. How the App Works**

This dashboard is a "Single Page Application." It is entirely self-contained within one file (itinerary\_planner.html). It does not require a web server to run—you can simply double-click the file to open it in Chrome, Safari, or Edge.

* **Styling:** It uses **Tailwind CSS** via a secure CDN link at the top of the file to handle all the layout, colors, and typography.  
* **Icons:** It uses **Lucide Icons** via a CDN link for the small graphics (ships, footprints, etc.).  
* **Data & Logic:** All the data (prices, times, descriptions) and the calculator logic are handled by plain JavaScript located inside the \<script\> tag near the bottom of the file.

## **2\. How to Update Tour Information**

If Oceania Cruises changes the price of a tour, or if your ship's arrival time changes, you can easily update the dashboard.

Open itinerary\_planner.html in a basic text editor (like Notepad on Windows or TextEdit/BBEdit on Mac, or a code editor like VS Code).

Scroll down to the \<script\> section. You will see a list called const ports \= \[ ... \]. Each port has its own block of data. It looks like this:

{  
    id: 'aberdeen',  
    name: 'Aberdeen, Scotland',  
    defaultChoice: 'excursion',  
    date: 'Wed, May 19',  
    arrive: '7:00 AM',  
    depart: '5:00 PM',  
    allAboard: '4:00 PM',  
    currency: '💷 GBP (£)',  
    excursion: {  
        code: 'ABE-002',  
        title: 'The Castle and the Coast',  
        price: 119, // \<--- UPDATE PRICE HERE  
        // ...  
    },  
    diy: {  
        // ...  
    }  
}

**To make changes:**

1. **Prices:** Find the price: 119 line for the specific port and change the number. *Do not add quotes or dollar signs around the number.*  
2. **Times:** Update the text inside the quotes for arrive, depart, or allAboard (e.g., change '7:00 AM' to '8:00 AM').  
3. **Text/Descriptions:** You can safely change any text inside the single quotes (e.g., the whyExcursion or highlights text).

## **3\. How to Update the Credit Limit**

If you miraculously get more onboard credit, you can update the calculator's limit.

1. Scroll down past the port data inside the \<script\> tag.  
2. Look for this line: const shoreCredit \= 300;  
3. Change 300 to your new amount. The dashboard will automatically recalculate everything.

## **4\. Managing the Images**

The dashboard is currently set up to look for local image files in the exact same folder as the HTML file.

* **File Naming:** It expects names like aberdeen-excursion.jpg and aberdeen-diy.jpg.  
* **Missing Images:** If the dashboard cannot find the image file, it has a built-in safety fallback that will display a clean gray box with a "Camera Off" icon. It will not break the page layout.  
* **Updating Images:** If you want to use your own photos, simply name your new photo exactly the same as the old one (e.g., cork-diy.jpg) and replace the file in the folder. Note that images with a **16:9 (landscape) aspect ratio** will look best.

## **5\. Pre-Travel Checklist (To Do in Early 2027\)**

Because you are planning far in advance, you should verify the following details roughly 60 days before you sail:

* \[ \] **Verify Excursion Prices:** Log into your Oceania Cruises portal and ensure the prices for your chosen tours (e.g., ABE-002, KOI-001) haven't increased. Update the HTML file if they have.  
* \[ \] **Verify Port Times:** Cruise itineraries frequently shift arrival and departure times by an hour or two based on port traffic. Check your final cruise documents and update the arrive, depart, and allAboard fields.  
* \[ \] **Check Restaurant Status:** Independent businesses can change. Verify on Google Maps that recommended spots (Bread 41 in Dublin, Farmgate Cafe in Cork) are still open and haven't changed their operating hours for the days you are visiting.  
* \[ \] **Test Google Maps Links:** Click the "View Full Route Map" buttons in the DIY guides to ensure Google hasn't altered its routing algorithms and that the paths still make sense.

## **6\. Print Mode**

If you want to print the itinerary, simply open itinerary\_planner.html in your web browser and press Ctrl+P (Windows) or Cmd+P (Mac).

The document contains special @media print CSS that will automatically:

* Remove dark background colors to save ink.  
* Hide the interactive buttons.  
* Hide the images to keep the document concise.  
* Expand the DIY step-by-step instructions so they are visible on the paper copy.