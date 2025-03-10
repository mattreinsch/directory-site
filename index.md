---
layout: default
title: AI Tools Directory
---
<head>
    <!-- Add the Google Fonts link here -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@900&display=swap" rel="stylesheet">
</head>
<!-- Main Container -->
<div class="container mx-auto px-4 py-6">

  <!-- Dark Mode Toggle -->
  <button onclick="toggleDarkMode()" class="mb-4 px-4 py-2 bg-gray-700 text-white rounded">
      🌙 Dark Mode
  </button>

  <!-- Title with custom font and larger size -->
  <h1 class="text-5xl font-extrabold text-center text-gray-900 mb-8">AI Tools Directory</h1>

  <!-- Search Bar -->
  <div class="mb-4">
      <input type="text" id="search" placeholder="Search AI tools..." class="w-full p-2 border rounded mb-4" onkeyup="filterTools()">
  </div>

  <!-- Filter by Category -->
  <div class="mb-4">
      <button onclick="filterCategory('All')" class="px-4 py-2 bg-gray-300 rounded mr-2">All</button>
      {% assign categories = site.data.tools | map: 'category' | uniq %}
      {% for category in categories %}
      <button onclick="filterCategory('{{ category }}')" class="px-4 py-2 bg-gray-300 rounded mr-2">{{ category }}</button>
      {% endfor %}
  </div>

  <!-- Tools Grid -->
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6" id="tools-container">
      {% for tool in site.data.tools %}
      <div class="bg-white p-4 rounded shadow-lg tool-card" data-category="{{ tool.category }}">
          <img src="{{ tool.image }}" alt="{{ tool.name }}" class="h-24 w-24 object-contain mb-4 mx-auto">
          <h2 class="text-lg font-bold text-center">{{ tool.name }}</h2>
          <p class="text-sm text-gray-600 text-center mb-2">{{ tool.category }}</p>
          <p class="text-sm text-gray-800 text-center mb-4">{{ tool.description }}</p>
          <div class="flex justify-center">
              <a href="{{ tool.website }}" class="text-blue-500 text-center" target="_blank">Visit Website</a>
          </div>
      </div>
      {% endfor %}
  </div>

  <!-- Pagination / Load More Button -->
  <div id="pagination" class="text-center mt-8">
      <button id="load-more" class="px-4 py-2 bg-blue-500 text-white rounded" onclick="loadMoreTools()">Load More Tools</button>
  </div>

  <!-- Call to Action -->
  <div class="mt-8 text-center">
      <h3 class="text-2xl font-bold mb-4">Submit a Tool</h3>
      <p>Have a great AI tool that we haven't listed yet? Submit it and get featured!</p>
      <a href="https://forms.google.com/your-form-link" class="mt-4 inline-block px-6 py-2 bg-green-500 text-white rounded">Submit a Tool</a>
  </div>

</div>

<script>
// Dark Mode Toggle
function toggleDarkMode() {
    document.body.classList.toggle("dark-mode");
}

// Filter Tools by Search Input
function filterTools() {
    let input = document.getElementById("search").value.toLowerCase();
    let cards = document.querySelectorAll(".tool-card");

    cards.forEach(card => {
        let name = card.querySelector("h2").textContent.toLowerCase();
        if (name.includes(input)) {
            card.style.display = "block";
        } else {
            card.style.display = "none";
        }
    });
}

// Filter Tools by Category
function filterCategory(category) {
    let cards = document.querySelectorAll(".tool-card");
    cards.forEach(card => {
        let cardCategory = card.getAttribute("data-category");
        if (category === 'All' || cardCategory === category) {
            card.style.display = "block";
        } else {
            card.style.display = "none";
        }
    });
}

// Pagination Logic (or Infinite Scroll)
let currentPage = 1;
const toolsPerPage = 6;
const tools = document.querySelectorAll(".tool-card");

function showPage(page) {
    const startIndex = (page - 1) * toolsPerPage;
    const endIndex = startIndex + toolsPerPage;

    tools.forEach((tool, index) => {
        if (index >= startIndex && index < endIndex) {
            tool.style.display = 'block';
        } else {
            tool.style.display = 'none';
        }
    });
}

function loadMoreTools() {
    currentPage++;
    showPage(currentPage);
}

// Initially load the first page
showPage(currentPage);
</script>

<style>
/* Dark Mode Styles */
body.dark-mode {
    background-color: #121212;
    color: white;
}

body.dark-mode .bg-white {
    background-color: #1e1e1e;
    color: white;
}

body.dark-mode .text-gray-600 {
    color: #b0b0b0;
}

body.dark-mode .text-blue-500 {
    color: #4fa3f7;
}

/* Tool Card Styling */
.tool-card {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.tool-card:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.tool-card img {
    border-radius: 50%;
    max-width: 100%;
    margin-bottom: 16px;
}

/* Pagination Styling */
#pagination button {
    padding: 10px 20px;
    background-color: #3498db;
    color: white;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    border: none;
}

#pagination button:hover {
    background-color: #2980b9;
}

/* Larger Title with Better Font */
h1 {
    font-family: 'Roboto', sans-serif;
    font-size: 4rem;
    font-weight: 900;
    color: #333;
    text-align: center;
    margin-bottom: 2rem;
}
</style>
