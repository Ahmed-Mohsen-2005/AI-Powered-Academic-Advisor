
# 🎓 48 Days Challenge – AI Academic Advisor

This project is part of the 48 Days Challenge to build a personalized academic advising system for students using AI. It models a real curriculum (CSAI – Zewail City) and simulates 100 students navigating course paths with constraints and AI-driven recommendations.

---

## 🧰 Features

- 📚 Curriculum graph with full course prerequisites using NetworkX
- 👩‍🎓 Simulation of 100 diverse students:
  - GPA, term history, interests
  - Grades and passed/failed records
- 📜 Course constraints enforced:
  - Max 3–5 courses per term
  - Prerequisite satisfaction
  - Retake policy for failed courses
- 🧠 Heuristic-Based Recommendation System

---

## 📊 Project Structure

```bash
48-days-ai-advisor/
├── curriculum_graph.py        # Builds the full course graph
├── simulate_students.py       # Generates 100 students
├── simulated_students.json    # Exported student data
├── heuristic_recommendations.json  # Output recommendation file
├── README.md                  # This file
```

---

## 🚀 How to Run

### 1. Install Dependencies

```bash
pip install networkx matplotlib numpy
```

### 2. Generate Curriculum Graph

```python
# curriculum_graph.py
from curriculum_graph import build_curriculum_graph
G = build_curriculum_graph()
```

### 3. Simulate Students

```bash
python simulate_students.py
```

### 4. Run Heuristic Recommendation

```bash
python heuristic_recommender.py
```

---

## 🧠 Heuristic Recommendation Logic

Each student receives a list of **3–5 eligible courses** per term based on:

- ✅ Prerequisite satisfaction
- ✅ Not previously taken
- ✅ Prioritization by **interest match** (e.g., AI, Security)

### 💡 Example Logic (Python)

```python
def recommend_courses_heuristic(student, curriculum, max_courses=5):
    completed = set(student["completed_courses"])
    interests = set(student["interests"])

    eligible_courses = [
        cid for cid, info in curriculum.items()
        if cid not in student["grades"] and
        all(pr in completed for pr in info["prerequisites"])
    ]

    def course_score(cid):
        category = curriculum[cid]["category"]
        return 1 if any(interest in category for interest in interests) else 0

    ranked_courses = sorted(eligible_courses, key=course_score, reverse=True)
    return ranked_courses[:min(len(ranked_courses), max_courses)]
```

---

## 📬 Sample Output

```json
{
  "student_id": 17,
  "GPA": 3.28,
  "interests": ["AI", "Software Engineering"],
  "recommended_courses": ["CSAI301", "SW302", "CSAI204"]
}
```

---

## 📚 Curriculum

Based on Zewail City’s CSAI curriculum, including:
- Core courses
- Software Development (SWD) major
- Prerequisite structure as a directed graph

---

## 📦 Future Extensions

- Export curriculum to Neo4j using Cypher
- Add elective paths (e.g., DSAI, IT)
- Visualize course maps per student
- Upgrade to ML or RL-based recommender (optional)

---

## 👨‍💻 Author

Developed for educational AI applications and personalized student planning as part of the 48 Days Challenge.
