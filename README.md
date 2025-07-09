# Dynamic-Pricing-for-Urban-Parking-Lots

## 💡 Overview
This project simulates real-time parking price optimization using static and demand-based models using PATHWAY and Bokeh.

⏱️ Real-time processing using Pathway
📊 Interactive price visualizations using Bokeh + Panel
🧠 Two intelligent pricing models: Baseline and Demand-Based
📈 Prices stay fair: always between 0.5x and 2x of the base price

## 🛠 Tech Stack
| **Component**        | **Tool / Library**       | **Role**                                       |
| -------------------- | ------------------------ | ---------------------------------------------- |
| **Notebook**         | Google Colab             | Development & demonstration environment        |
| **Real-time Engine** | Pathway                  | Stream processing, time-windowed feature logic |
| **Visualization**    | Bokeh + Panel (optional) | Interactive, real-time pricing plots           |
| **Data Handling**    | Pandas, NumPy            | Data transformation, feature engineering       |
| **Storage**          | CSV, JSONL               | Input stream & continuous output storage       |

## 🧠 Models Implemented
1. **Model 1 – Static Pricing**: Price increases cumulatively with occupancy.
2. **Model 2 – Demand-Based**: Price adapts to real-time demand (occupancy, traffic, queue, etc.)

## 📊 Visualizations
All outputs are generated using Bokeh: time-based price plots for each parking lot.

## 🔁 Real-Time Simulation
Pathway streams historical data (`dataset.csv`) with preserved timestamps. Pricing is computed and emitted in real-time.

## 🧱 Architecture
            ┌──────────────────┐
            │  dataset.csv     │  ← Original parking data
            └────────┬─────────┘
                     │
         ┌───────────▼────────────┐
         │ Pathway Ingestion      │  ← Reads data using schema
         │ (Static/Streaming)     │
         └───────────┬────────────┘
                     │
        ┌────────────▼──────────────┐
        │ Feature Engineering       │
        │ - OccupancyRate           │
        │ - Queue, Traffic, Vehicle│
        └────────────┬──────────────┘
                     │
      ┌──────────────▼───────────────┐
      │   Pricing Logic (Model 1/2)  │
      │   Static or Demand-Based     │
      └──────────────┬───────────────┘
                     │
         ┌───────────▼─────────────┐
         │ Output (CSV/JSONL)      │  ← pricing_output.jsonl, model2_stream_output.csv
         └───────────┬─────────────┘
                     │
         ┌───────────▼─────────────┐
         │    Pandas + Bokeh       │  ← Real-time plots per lot
         └─────────────────────────┘


### Data Flow Diagram:

                        ┌─────────────────────┐
                        │     dataset.csv     │
                        └────────┬────────────┘
                                 │
                                 ▼
                   ┌─────────────────────────────┐
                   │     Pathway Streaming Engine │
                   │  (real-time timestamp flow)  │
                   └────────┬─────────────┬───────┘
                            │             │
             ┌──────────────▼──┐     ┌────▼────────────────┐
             │   Model 1:      │     │   Model 2:           │
             │ Static Pricing  │     │ Demand-Based Pricing│
             └──────┬──────────┘     └──────────┬──────────┘
                    │                           │
          ┌─────────▼─────────┐       ┌─────────▼────────────────────┐
          │ Compute price via │       │ Feature Engineering:         │
          │ OccupancyRate     │       │ - Occupancy Rate             │
          │ Pricet+1 = ...    │       │ - Queue, Traffic, Vehicle... │
          └─────────┬─────────┘       └─────────┬────────────────────┘
                    │                           │
          ┌─────────▼─────────────┐   ┌─────────▼────────────────────┐
          │ pricing_output.jsonl  │   │ model2_stream_output.csv     │
          └─────────┬─────────────┘   └─────────┬────────────────────┘
                    │                           │
       ┌────────────▼──────────────┐ ┌──────────▼──────────────┐
       │  Bokeh Visuals (per lot)  │ │ Real-Time Bokeh Graphs  │
       └───────────────────────────┘ └──────────────────────────┘





