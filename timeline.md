---
layout: page
title: Timeline
permalink: /timeline/
description: "PhD journey & life milestones"
# Optional: uncomment if your theme supports header images
header-img: img/bg-walle.jpg 
---

<!--
HOW TO USE
1) Save this file as timeline.html (or timeline.md) inside your Jekyll site.
2) Adjust the front matter above to match your theme (e.g., layout: page/post).
3) Replace events[] below with your real milestones.
4) (Optional) Move images into /img/timeline/... and update paths accordingly.

Notes
- This is a self-contained page: no external CSS/JS needed.
- It supports filtering by category (PhD, Research, Publications, Teaching, Travel, Sports, Personal...) and free‑text search.
- It auto-sorts by date (newest first) and groups by year.
- Deep-linking: you can use ?cat=PhD or ?q=paper to pre-filter/search.
-->

<style>
  :root {
    --bg: #ffffff;
    --card: #ffffff;
    --text: #1a1a1a;
    --muted: #6b7280;
    --line: #e5e7eb;
    --accent: #2563eb; /* link/active */
    --chip: #f3f4f6;
    --shadow: 0 10px 20px rgba(0,0,0,0.06), 0 2px 6px rgba(0,0,0,0.06);
    --radius: 16px;
  }

  /* Page shell */
  .tl-wrap {
    max-width: 980px;
    margin: 0 auto;
    padding: 24px 18px 60px;
    color: var(--text);
    background: var(--bg);
  }
  .tl-header {
    display: grid;
    gap: 14px;
    margin-bottom: 18px;
  }
  .tl-title { font-size: clamp(28px, 2.6vw, 40px); font-weight: 800; letter-spacing: -0.01em; }
  .tl-sub { color: var(--muted); max-width: 70ch; }

  /* Controls */
  .tl-controls { display: flex; flex-wrap: wrap; gap: 10px; align-items: center; margin-top: 6px; }
  .tl-search { flex: 1 1 280px; }
  .tl-search input {
    width: 100%; padding: 10px 12px; border: 1px solid var(--line); border-radius: 12px; outline: none;
  }
  .tl-chips { display: flex; flex-wrap: wrap; gap: 8px; }
  .chip {
    padding: 8px 12px; border-radius: 999px; background: var(--chip); border: 1px solid var(--line);
    font-size: 14px; cursor: pointer; user-select: none; transition: background 0.2s, color 0.2s, border 0.2s;
  }
  .chip.active { background: rgba(37,99,235,0.08); color: var(--accent); border-color: rgba(37,99,235,0.35); }

  /* Timeline */
  .timeline { position: relative; margin-top: 24px; }
  .year-group { margin: 32px 0 10px; font-weight: 800; font-size: 22px; }
  .line {
    position: absolute; left: 26px; top: 0; bottom: 0; width: 2px; background: linear-gradient(180deg, var(--line), #fff);
  }

  .item { display: grid; grid-template-columns: 52px 1fr; gap: 14px; margin: 18px 0; }
  .dot { position: relative; width: 12px; height: 12px; border-radius: 50%; background: var(--accent); margin-top: 10px; box-shadow: 0 0 0 4px rgba(37,99,235,0.15); }
  .date { color: var(--muted); font-size: 13px; margin-top: 4px; }

  .card {
    background: var(--card); border: 1px solid var(--line); border-radius: var(--radius); box-shadow: var(--shadow);
    padding: 16px; display: grid; gap: 10px;
  }
  .card h3 { margin: 0; font-size: 18px; }
  .meta { color: var(--muted); font-size: 13px; display: flex; gap: 12px; flex-wrap: wrap; }
  .desc { line-height: 1.6; }
  .thumb {
    width: 100%; aspect-ratio: 16/9; object-fit: cover; border-radius: 12px; border: 1px solid var(--line);
    cursor: zoom-in;
  }
  .badge { font-size: 12px; padding: 6px 9px; background: var(--chip); border: 1px solid var(--line);
           border-radius: 999px; }
  .badges { display: flex; flex-wrap: wrap; gap: 6px; }

  .empty { text-align: center; color: var(--muted); padding: 28px; border: 1px dashed var(--line); border-radius: 12px; }

  /* Lightbox */
  .lightbox { position: fixed; inset: 0; background: rgba(0,0,0,0.6); display: none; align-items: center; justify-content: center; padding: 20px; }
  .lightbox img { max-width: 95vw; max-height: 85vh; border-radius: 12px; border: 2px solid #fff; }

  @media (max-width: 560px) {
    .line { left: 22px; }
    .item { grid-template-columns: 44px 1fr; }
  }
</style>

<div class="tl-wrap" id="timeline-root">
  <div class="tl-header">
    <div>
      <div class="tl-title">Personal Timeline</div>
      <div class="tl-sub">A visual log of my PhD journey and life milestones: research, publications, teaching, conferences, and the detours that shaped the path.</div>
    </div>

    <div class="tl-controls">
      <div class="tl-search"><input id="searchInput" type="search" placeholder="Search (e.g., ‘paper’, ‘Trondheim’, ‘CCUS’)"></div>
      <div class="tl-chips" id="chipRow">
        <!-- Chips will be injected. Default set lives in JS below. -->
      </div>
    </div>
  </div>

  <div class="timeline">
    <div class="line"></div>
    <div id="timeline"></div>
  </div>
</div>

<!-- Lightbox for images -->
<div class="lightbox" id="lightbox" aria-hidden="true" role="dialog">
  <img alt="Expanded timeline image" />
</div>

<script>
  // ===== 1) Editable data =====
  // Replace with your real milestones. Keep ISO dates (YYYY-MM-DD) for proper sorting.
  const events = [
    {
      date: "2022-08",
      title: "Started PhD & Journey in Vienna",
      location: "Vienna, AT",
      categories: ["PhD", "Journey"],
      description: "xxx",
      image: "/img/timeline/Vienna2022.jpg",
      alt: "Vienna Donau"
    },
     {
      date: "2022-11",
      title: "Visited DTU & Denmark finally",
      location: "Copenhagen, DK",
      categories: ["Travel", "Journey"],
      description: "xxx",
      image: "/img/timeline/Vienna2022.jpg",
      alt: "Vienna Donau"
    },
      {
      date: "2023-03",
      title: "Completed my first top-rope climbing lessons",
      location: "Vienna, AT",
      categories: ["Sports", "Personal","Journey"],
      description: "xxx",
      image: "/img/timeline/Vienna2022.jpg",
      alt: "Vienna Donau"
    },
    {
      date: "2023-05",
      title: "First GRC & GRS Conference about CCUS",
      location: "Les Diablerets, CH",
      categories: ["Conference", "Research","PhD","Journey"],
      description: "xxx",
      image: "/img/post-bg-halting.jpg",
      alt: "Presenter at a conference podium"
    },
    {
      date: "2023-07",
      title: "First Summer trips in Italy and Basque",
      location: "Italy",
      categories: ["Travel","Personal","Journey"],
      description: "xxx",
      image: "/img/post-bg-web.jpg",
      alt: "Trip in Italy"
    },
    {
      date: "2023-10",
      title: "Autumn School about Brightway & LCA ",
      location: "Energy & AI (under review)",
      categories: ["PhD", "Studying","Research","Journey"],
      description: "xxx",
      image: "/img/post-bg-2015.jpg",
      alt: "Working photo"
    },
    {
      date: "2024-01",
      title: "Travel in China with my boyfriend",
      location: "Beijing, CN",
      categories: ["Travel","Personal", "Journey"],
      description: "xxx",
      image: "/img/post-bg-alitrip.jpg",
      alt: "Selfie in Beijing"
    },
    {
      date: "2024-04",
      title: "Completed review paper about prospective assessments",
      location: "doi",
      categories: ["Publications", "PhD","Research","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
    {
      date: "2024-06",
      title: "First presentation at ESCAPE34",
      location: "Florence, IT",
      categories: ["Publications", "PhD","Research","Conference","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
    {
      date: "2024-08",
      title: "Bornout and 'Lost'",
      location: "Vienna, AT",
      categories: ["Personal","PhD","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
    {
      date: "2024-10",
      title: "Autumn School about Energy systems modelling",
      location: "Gothenburg, SE",
      categories: ["Studying","PhD","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
    {
      date: "2024-02",
      title: "Completed my skiing lessons at Alps",
      location: "Bad Gastein, AT",
      categories: ["Sports","Personal","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
    {
      date: "2024-04",
      title: "First Conference and Trip in California",
      location: "Palm Spring, CA",
      categories: ["PhD","Conference","Personal","Journey"],
      description: "xxx",
      image: "/img/timeline/USA2025.jpg",
      alt: "arXiv logo on a screen"
    }
    {
      date: "2024-08",
      title: "Summer trip in Italy and Rebuilding",
      location: "Sardinia, IT",
      categories: ["Personal","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
     {
      date: "2024-10",
      title: "JuliaCon Paris and trip",
      location: "Paris, FR",
      categories: ["Conference","Travel","Personal","Journey"],
      description: "xxx",
      image: "/img/post-bg-digital-native.jpg",
      alt: "arXiv logo on a screen"
    }
  ];

  // Default categories available as filter chips. Add/remove to match your needs.
  const defaultChips = ["All", "Journey","PhD", "Research", "Publications", "Conference", "Studying","Workshop","Travel", "Sports","Personal", "Buronout"];

  // ===== 2) Utility functions =====
  const qs = (sel, el=document) => el.querySelector(sel);
  const qsa = (sel, el=document) => Array.from(el.querySelectorAll(sel));
  const fmtDate = (iso) => new Date(iso).toLocaleDateString(undefined, { year: 'numeric', month: 'short', day: '2-digit' });
  const byDateDesc = (a,b) => new Date(b.date) - new Date(a.date);
  const getYear = (iso) => new Date(iso).getFullYear();

  // Parse URL params for deep-linking
  const url = new URL(window.location);
  const initCat = url.searchParams.get('cat') || 'All';
  const initQuery = url.searchParams.get('q') || '';

  // ===== 3) Render chips =====
  const chipRow = qs('#chipRow');
  let activeCat = initCat;
  defaultChips.forEach(cat => {
    const b = document.createElement('button');
    b.className = 'chip' + (cat === activeCat ? ' active' : '');
    b.textContent = cat;
    b.setAttribute('data-cat', cat);
    b.addEventListener('click', () => {
      activeCat = cat;
      qsa('.chip', chipRow).forEach(c => c.classList.remove('active'));
      b.classList.add('active');
      render();
      const p = new URLSearchParams(url.search);
      p.set('cat', activeCat);
      history.replaceState({}, '', `${url.pathname}?${p.toString()}`);
    });
    chipRow.appendChild(b);
  });

  // ===== 4) Search box =====
  const searchInput = qs('#searchInput');
  searchInput.value = initQuery;
  searchInput.addEventListener('input', () => {
    const p = new URLSearchParams(url.search);
    p.set('q', searchInput.value);
    history.replaceState({}, '', `${url.pathname}?${p.toString()}`);
    render();
  });

  // ===== 5) Lightbox =====
  const lb = qs('#lightbox');
  lb.addEventListener('click', () => { lb.style.display = 'none'; lb.setAttribute('aria-hidden', 'true'); });

  function openLightbox(src, alt) {
    const img = lb.querySelector('img');
    img.src = src; img.alt = alt || '';
    lb.style.display = 'flex';
    lb.setAttribute('aria-hidden', 'false');
  }

  // ===== 6) Main render =====
  function render() {
    const root = qs('#timeline');
    root.innerHTML = '';

    const term = searchInput.value.trim().toLowerCase();
    const filtered = events
      .slice()
      .sort(byDateDesc)
      .filter(ev => {
        const matchCat = (activeCat === 'All') || (ev.categories || []).includes(activeCat);
        if (!matchCat) return false;
        if (!term) return true;
        const hay = [ev.title, ev.location, ev.description, ...(ev.categories||[])].join(' ').toLowerCase();
        return hay.includes(term);
      });

    if (!filtered.length) {
      const empty = document.createElement('div');
      empty.className = 'empty';
      empty.textContent = 'No items match your filters. Try another category or search term.';
      root.appendChild(empty);
      return;
    }

    let currentYear = null;
    filtered.forEach(ev => {
      const y = getYear(ev.date);
      if (y !== currentYear) {
        currentYear = y;
        const yg = document.createElement('div');
        yg.className = 'year-group';
        yg.textContent = y;
        root.appendChild(yg);
      }

      const item = document.createElement('div');
      item.className = 'item';

      const colL = document.createElement('div');
      const dot = document.createElement('div'); dot.className = 'dot';
      const date = document.createElement('div'); date.className = 'date'; date.textContent = fmtDate(ev.date);
      colL.appendChild(dot); colL.appendChild(date);

      const colR = document.createElement('div');
      const card = document.createElement('div'); card.className = 'card';

      const h3 = document.createElement('h3'); h3.textContent = ev.title; card.appendChild(h3);

      const meta = document.createElement('div'); meta.className = 'meta';
      if (ev.location) {
        const loc = document.createElement('div'); loc.textContent = '📍 ' + ev.location; meta.appendChild(loc);
      }
      if (ev.categories && ev.categories.length) {
        const cats = document.createElement('div'); cats.className = 'badges';
        ev.categories.forEach(c => {
          const b = document.createElement('span'); b.className = 'badge'; b.textContent = c; cats.appendChild(b);
        });
        meta.appendChild(cats);
      }
      card.appendChild(meta);

      if (ev.image) {
        const img = document.createElement('img');
        img.className = 'thumb';
        img.src = ev.image; img.alt = ev.alt || '';
        img.addEventListener('click', () => openLightbox(ev.image, ev.alt));
        card.appendChild(img);
      }

      if (ev.description) {
        const p = document.createElement('div'); p.className = 'desc'; p.textContent = ev.description; card.appendChild(p);
      }

      colR.appendChild(card);

      item.appendChild(colL);
      item.appendChild(colR);
      root.appendChild(item);
    });
  }

  // Initial render
  render();
</script>