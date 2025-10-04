"mermaid
flowchart LR
  %% MabuHighTrack – End-to-End Activity (Mermaid)
  %% Swimlanes are approximated with subgraphs

  subgraph ADMIN["Administrator"]
    A1["Register teacher & student accounts"]
    A2["Set school year / semester"]
    A3["Configure subjects / sections"]
  end

  subgraph SYS["System"]
    S1["Create user records and send credentials"]
    S2{"Credentials valid?"}
    S3["Validate input completeness"]
    S4{"Data complete?"}
    S5["Persist grades & attendance"]
    S6["Run performance prediction (LightGBM)"]
    S7["Store / update prediction results"]
    S8["Recompute prediction if data changed"]
    S9["Update dashboards & reports"]
  end

  subgraph STUD["Student"]
    U1["Receive credentials • log in"]
    U2["View profile / dashboard"]
    U3["Error: invalid credentials"]
    U4["View grades & attendance"]
    U5["View predicted performance / risk"]
    U6{"Wants clarification?"}
    U7["Submit concern / request"]
  end

  subgraph TEACH["Subject Teacher"]
    T1["Input or edit grades: WW, PT, QA"]
    T2["Record attendance"]
    T3["Verify records after concern"]
    T4{"Correction needed?"}
    T5["Edit entries then resave"]
    T6["Send explanation to student"]
  end

  subgraph ADV["Adviser"]
    D1["Open advisory class dashboard"]
    D2["Download or print advisory report"]
  end

  subgraph PRIN["Principal"]
    P1["Open analytics dashboard"]
    P2["Review school-wide reports: grades, attendance, at-risk, trends"]
  end

  %% Flow
  A1 --> A2 --> A3 --> S1
  S1 --> U1 --> S2
  S2 -- "Yes" --> U2
  S2 -- "No"  --> U3 --> U1

  T1 --> T2 --> S3
  S3 --> S4
  S4 -- "Yes" --> S5 --> S6 --> S7
  S4 -- "No"  --> T1

  U2 --> U4 --> U5 --> U6
  U6 -- "Yes" --> U7 --> T3
  U6 -- "No"  --> S9

  T3 --> T4
  T4 -- "Yes" --> T5 --> S8 --> S9
  T4 -- "No"  --> T6 --> S9

  D1 --> D2
  P1 --> P2

  S9 --> A3  %% end-of-cycle admin review"
