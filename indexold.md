---
layout: default
title: AI Tools Directory
---

<input type="text" id="search" placeholder="Search tools..." class="w-full p-2 border rounded mb-4" onkeyup="filterTools()">

<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
  {% for tool in site.data.tools %}
  <div class="bg-white p-4 rounded shadow">
      <h2 class="text-lg font-bold">{{ tool.name }}</h2>
      <p class="text-sm text-gray-600">{{ tool.category }}</p>
      <a href="{{ tool.website }}" class="text-blue-500" target="_blank">Visit Website</a>
  </div>
  {% endfor %}
</div>

<script>
function filterTools() {
    let input = document.getElementById("search").value.toLowerCase();
    let cards = document.querySelectorAll(".bg-white");

    cards.forEach(card => {
        let name = card.querySelector("h2").textContent.toLowerCase();
        if (name.includes(input)) {
            card.style.display = "block";
        } else {
            card.style.display = "none";
        }
    });
}
</script>

