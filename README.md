🚇 Smart City Multimodal Mobility - STN_003 Investigation
📊 Project Overview
This project investigates a reported "hardware failure" at subway station STN_003 using three independent datasets to determine if the failure was real or caused by external factors.

Question: Did STN_003 suffer a hardware failure, or did something else happen?

📁 Datasets
File	Description	Records
scooter_rides.csv	E-scooter trip records across the city	~5,000
subway_turnstile.csv	Hourly turnstile counts across 10 stations	~2,000
city_heartbeat.json	30 days of weather and civic sensor data	30 days
🛠️ Tools
Python 3.x

Pandas, NumPy

Matplotlib/Seaborn

Regular Expressions

🔄 Analysis Phases
Phase 1: Data Cleaning
Standardized station IDs (strip spaces, uppercase)

Cleaned coordinates (removed °, N, S, E, W)

Cast data types (battery, ratings, timestamps)

Handled negative turnstile counts (absolute value)

Phase 2: Aggregation
Daily station totals and hourly averages

STN_003 bounding box (±0.006° lat/lng) for scooter isolation

Phase 3: Pivot Table
Day-15 pivot table (hours × stations)

Identified STN_003 as the only unusual station

Phase 4: Visualization
3-panel chart: subway entries, scooter rides, precipitation

Shaded disputed period (14:00-20:00)

📈 Key Findings
Subway: 75% drop in STN_003 entries (14:00-17:00)

Scooter: 66% decrease in rides near STN_003

Weather: 59.4mm rain on Day 15

Other Stations: Normal activity

🎯 Final Verdict
NO hardware failure. The event was a weather-related disruption:

Heavy rain reduced passenger volume

Low volume triggered sensor thresholds

Both subway and scooter activity recovered after rain subsided

🚀 Quick Start
bash
pip install pandas numpy matplotlib seaborn
python stn003_investigation.py
Outputs:

stn003_investigation.png - Multi-panel visualization

stn003_verdict.txt - Final verdict with recommendations

📝 Key Code Patterns
python
# Clean station IDs
df['station_id'] = df['station_id'].str.strip().str.upper()

# Bounding box
df['in_stn003_box'] = (
    (df['lat'] >= 40.7128 - 0.006) & (df['lat'] <= 40.7128 + 0.006) &
    (df['lng'] >= -74.0060 - 0.006) & (df['lng'] <= -74.0060 + 0.006)
)

# Pivot table
pivot = df.pivot_table(index='hour', columns='station_id', values='entries', aggfunc='sum')

# 3-panel visualization
fig, axes = plt.subplots(3, 1, figsize=(14, 12), sharex=True)
🎓 Learning Outcomes
Data cleaning for real-world messy data

Multi-source validation

Pivot table analysis

Multi-panel visualization

Critical thinking in data investigation

👩‍💻 Author
Rida Hafeez
