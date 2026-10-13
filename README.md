# TravelPlanner AI – Intelligent Travel Planning Using Classical AI

> **Tagline:** Intelligent Travel Planning Using Classical Artificial Intelligence  
> **Academic Focus:** Fundamentals of Artificial Intelligence (Knowledge Representation, Constraint Satisfaction, Search Algorithms, Heuristics, and Rule-Based Reasoning)

---

## 🚫 ZERO MACHINE LEARNING GUARANTEE

This application strictly contains **NO Machine Learning, Deep Learning, Neural Networks, Embeddings, Model Training, or LLM-based recommendation engines**.

All intelligence, decision-making, route sequencing, constraint checking, and itinerary optimizations are achieved entirely using **Classical Artificial Intelligence techniques**:
1. **Knowledge Representation (Ontology & Spatial Graphs)**
2. **Constraint Satisfaction Problems (CSP)**
3. **Classical Graph Search Algorithms (A\*, UCS, BFS, DFS)**
4. **Deterministic Heuristic Evaluation Functions**
5. **Forward-Chaining Production Rule Systems**

---

## 🏗️ PROJECT ARCHITECTURE

```text
FOAI/
├── backend/
│   ├── main.py                     # FastAPI application & static server
│   ├── database/
│   │   ├── schema.sql              # Relational SQLite schema
│   │   ├── seed_data.py            # Indian travel knowledge seeder
│   │   └── db.py                   # Data access queries & connection manager
│   ├── ai_engine/
│   │   ├── knowledge/
│   │   │   └── knowledge_base.py   # Spatial topology & Haversine distance
│   │   ├── constraints/
│   │   │   └── csp_solver.py       # Hard/Soft constraints & relaxation logic
│   │   ├── search/
│   │   │   └── search_engine.py    # A*, UCS, BFS, DFS with telemetry
│   │   ├── heuristics/
│   │   │   └── heuristic_evaluator.py # Explainable multi-factor scoring
│   │   ├── rules/
│   │   │   └── rule_engine.py      # Forward-chaining expert production rules
│   │   └── optimizer/
│   │       └── itinerary_generator.py # Master 3-plan synthesis orchestrator
│   ├── models/
│   │   └── schemas.py              # Pydantic request/response contracts
│   ├── routes/
│   │   └── api.py                  # API endpoints (/api/plan, /api/search-comparison)
│   └── tests/
│       └── test_all.py             # Full unit & integration test suite
├── frontend/
│   ├── index.html                  # Main SPA interface
│   ├── css/
│   │   └── style.css               # Modern travel-tech design system & dark navy theme
│   └── js/
│       ├── app.js                  # Master coordinator & demo launcher
│       ├── planner.js              # Multi-step wizard & validations
│       ├── aiVisualizer.js         # Animated 10-step reasoning visualizer
│       ├── itineraryView.js        # Day timeline & plan switcher
│       ├── mapView.js              # Leaflet OSM numbered routing map
│       ├── budgetManager.js        # Chart.js INR breakdown & progress
│       └── classicalAiHub.js       # Live search algorithm viva simulator
├── README.md                       # Complete viva & run guide
└── requirements.txt                # Python dependencies
```

---

## ⚡ QUICK START & INSTALLATION

### 1. Prerequisites
- Python 3.10+ (Python 3.14 supported)

### 2. Dependencies
Create or install packages:
```bash
python -m pip install fastapi uvicorn pydantic requests jinja2
```

### 3. Run the Application
Start the unified full-stack server:
```bash
python -m uvicorn backend.main:app --host 127.0.0.1 --port 8000 --reload
```
Open your browser and navigate to:
```text
http://127.0.0.1:8000
```

### 4. Run the Unit & Integration Tests
Execute all Classical AI unit tests:
```bash
python -m unittest backend/tests/test_all.py
```

---

## 🧠 HOW THE CLASSICAL AI ENGINES WORK

### 1. Knowledge Representation
- **Destinations:** Stored with geographical coordinates $(\text{lat}, \text{lon})$, climate, average stay duration, and popularity score.
- **Attractions:** Stored with category, opening/closing operating windows, recommended duration, admission fees (₹), and family safety flags.
- **Spatial Topology:** Adjacency edges computed using great-circle **Haversine Distance**:
  $$d = 2R \arcsin \left( \sqrt{\sin^2\left(\frac{\Delta \phi}{2}\right) + \cos(\phi_1)\cos(\phi_2)\sin^2\left(\frac{\Delta \lambda}{2}\right)} \right)$$

### 2. Constraint Satisfaction Problem (CSP)
- **Variables:** Daily time slots $\text{Slot}_{d, s}$ for day $d$ and slot $s \in \{\text{Morning}, \text{Afternoon}, \text{Sunset}, \text{Evening}\}$, Hotel $H$, Inter-city Transit $T$.
- **Domains:** Filtered attractions satisfying safety, pace limits, and excluded place constraints.
- **Hard Constraints:**
  - $\sum \text{Cost} \le \text{UserBudget}$
  - $\text{DailyTravelTime} \le T_{\text{max}}$
  - $T_{\text{open}} \le t_{\text{start}} < t_{\text{end}} \le T_{\text{close}}$
  - $\text{RequiredPlaces} \subseteq \text{Itinerary}$
  - $\text{ExcludedPlaces} \cap \text{Itinerary} = \emptyset$

### 3. Classical Search Algorithms
- **Breadth First Search (BFS):** Explores shortest hop count using a FIFO queue.
- **Depth First Search (DFS):** Backtracking search on permutation branches.
- **Uniform Cost Search (UCS / Dijkstra):** Priority queue min-heap ordered by accumulated actual path cost $g(n)$. Guarantees cheapest path.
- **A\* Search:** Priority queue ordered by evaluation function:
  $$f(n) = g(n) + h(n)$$
  where $g(n)$ is the accumulated road distance/cost, and $h(n)$ is the **admissible straight-line Haversine lower bound** to remaining unvisited target attractions. Because straight-line distance never overestimates true road distance ($h(n) \le h^*(n)$), $A^*$ is **admissible and globally optimal**.

### 4. Deterministic Heuristic Scoring
Candidate itineraries are scored on a scale of 0–100 via:
$$\text{Score} = w_1 \cdot S_{\text{interest}} + w_2 \cdot S_{\text{route}} + w_3 \cdot S_{\text{budget}} + w_4 \cdot S_{\text{time}} + w_5 \cdot S_{\text{pref}} - \text{Penalties}$$
- **$S_{\text{interest}}$ (0–30 pts):** Percentage of candidate attractions matching user interests.
- **$S_{\text{route}}$ (0–25 pts):** Spatial compactness and proximity efficiency.
- **$S_{\text{budget}}$ (0–20 pts):** Budget compliance and surplus buffer safety.
- **$S_{\text{time}}$ (0–15 pts):** Rest-to-activity balance per day.
- **$S_{\text{pref}}$ (0–10 pts):** Hotel category & transport mode match.

### 5. Forward-Chaining Rule-Based Expert System
Production rules evaluated in working memory:
- `IF budget_per_day < ₹2000 THEN force_hotel('Budget') AND prioritize_train()`
- `IF pace == 'Relaxed' THEN cap_activities(2) AND extend_duration(2.5h)`
- `IF pace == 'Fast-paced' THEN set_capacity(4, 5) AND apply_nearest_neighbor()`
- `IF travelers >= 3 OR interest == 'Family' THEN enforce_family_friendly(True)`
- `IF travelers >= 4 AND transport == 'Car' THEN recommend_group_suv()`

---

## 🎯 DEMO PRESETS (COLLEGE VIVA DEMO)

Clicking any demo button on the home page automatically loads and synthesizes:
1. **Chennai → Ooty:** 3 Days, ₹15,000, Nature & Mountain, Balanced pace (A* Search).
2. **Chennai → Goa:** 4 Days, ₹25,000, Beach & Nightlife, Fast pace (A* Search).
3. **Bengaluru → Mysuru:** 2 Days, ₹10,000, Royal Heritage & Family, Relaxed pace (UCS Search).
4. **Delhi → Jaipur:** 3 Days, ₹18,000, Pink City Heritage & Food, Balanced pace (A* Search).

---

## 🎓 VIVA QUESTIONS & ANSWERS CHEATSHEET

1. **Q: Why is this system Classical AI and not Machine Learning?**  
   *A:* In ML, systems learn patterns statistically from training data using weights and loss gradients. In Classical AI (Symbolic AI), decisions are made through explicit Knowledge Representation, deterministic search algorithms (BFS, DFS, UCS, A*), mathematical constraint satisfaction (CSP), and IF-THEN production rules.

2. **Q: Why is your A\* heuristic admissible?**  
   *A:* Our heuristic $h(n)$ computes the straight-line Haversine distance to unvisited destinations. The shortest distance between two points on a sphere is the great-circle arc. Since actual road distance is always $\ge$ straight-line distance, $h(n) \le h^*(n)$, guaranteeing that $h(n)$ never overestimates the true remaining cost.

3. **Q: How does UCS differ from A\* in your routing?**  
   *A:* UCS expands nodes in order of accumulated cost $g(n)$ without looking ahead to the goal. A* uses $f(n) = g(n) + h(n)$ to direct search towards the goal, expanding fewer nodes while maintaining identical optimality.
