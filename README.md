# 🏫 MabuHighTrack – Diagrams

This repo shows how to render Mermaid diagrams directly on **GitHub**.

- 📄 **Use Case / Activity Diagram (Markdown page):** [`diagrams/usecase-activity.md`](diagrams/usecase-activity.md)
- 🖼️ **Auto-exported SVG (via GitHub Actions):** `diagrams/usecase-activity.svg` (generated after your first push)

## Quick Start
1. Create a new GitHub repo and upload this folder.
2. Open `diagrams/usecase-activity.md` on GitHub → it **renders**.
3. Optional: the included GitHub Action exports `usecase-activity.mmd` to **SVG** on each push.

---

## Inline preview

flowchart LR
  %% MabuHighTrack – Use Case Diagram (Mermaid approximation)

  subgraph SYS["MabuhighTrack System"]
    U1(["View Grades & Attendance"])
    U2(["View Predicted Academic Performance"])
    U3(["Edit Sociodemographic information"])
    CORE(["Student Performance Prediction"])

    T1(["Input & Edit Grades (assigned subjects)"])
    T2(["View student sociodemographic info"])
    T3(["View predicted performance for assigned subject"])

    A1(["View Advisory Class Student Details"])
    A2(["View Advisory Class Grades & Attendance"])

    AD1(["Register Teachers & Student Account"])
    AD2(["View all grades, predictions & other data"])
    AD3(["Print Reports"])

    P1(["Review Reports / Analytics"])
  end

  Student[[Student]] --> U1
  Student[[Student]] --> U2
  Student[[Student]] --> U3
  U2 -. include .-> CORE

  Teacher[[Subject Teacher]] --> T1
  Teacher[[Subject Teacher]] --> T2
  Teacher[[Subject Teacher]] --> T3
  T3 -. include .-> CORE

  Adviser[[Adviser]] --> A1
  Adviser[[Adviser]] --> A2
  A2 -. include .-> CORE

  Administrator[[Administrator]] --> AD1
  Administrator[[Administrator]] --> AD2
  Administrator[[Administrator]] --> AD3
  AD2 -. include .-> CORE
  AD3 -. include .-> AD2

  Principal[[Principal]] --> P1
  P1 -. include .-> AD2
