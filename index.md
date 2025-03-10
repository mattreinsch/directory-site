---
layout: default
title: AI Tools Directory
---

<!-- Dark Mode Toggle -->
<button onclick="toggleDarkMode()" class="mb-4 px-4 py-2 bg-gray-700 text-white rounded">
    🌙 Dark Mode
</button>

<!-- Search Bar -->
<input type="text" id="search" placeholder="Search tools..." class="w-full p-2 border rounded mb-4" onkeyup="filterTools()">

<!-- Category Filter Buttons -->
<div class="mb-4">
    <button onclick="filterCategory('All')" class="px-4 py-2 bg-gray-300 rounded mr-2">All</button>
    {% assign categories = site.data.tools | map: 'category' | uniq %}
    {% for category in categories %}
    <button onclick="filterCategory('{{ category }}')" class="px-4 py-2 bg-gray-300 rounded mr-2">{{ category }}</button>
    {% endfor %}
</div>

<!-- Tools Grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6" id="tools-container">
    {% for tool in site.data.tools %}
    <div class="bg-white p-4 rounded shadow tool-card" data-category="{{ tool.category }}">
        <h2 class="text-lg font-bold">{{ tool.name }}</h2>
        <p class="text-sm text-gray-600">{{ tool.category }}</p>
        <a href="{{ tool.website }}" class="text-blue-500" target="_blank">Visit Website</a>
    </div>
    {% endfor %}
</div>

<!-- Script for Functionality -->
<script>
// Toggle Dark Mode
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
</script>

<!-- Style for Dark Mode and Layout -->
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

/* Tool Card Hover */
.tool-card:hover {
    transform: scale(1.05);
    transition: transform 0.2s;
}
</style>
