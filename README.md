
<p align="center">
  <img src="https://github.com/user-attachments/assets/6927d353-19c2-4841-b34f-2949e5a8264a" alt="Alt text description">
<p align="center">
  <strong>Natural Disaster Risk Intelligence Platform</strong><br>
  Real-Time Multi-Hazard Risk Assessment for Real Estate Portfolios
</p>  
<br>

A production-grade data pipeline that ingests real-time data from government APIs (USGS, NASA, NOAA) to assess natural disaster risk across earthquakes, wildfires, and severe weather.

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)

##  Business Problem

Real estate investors and Insurance companies need comprehensive risk assessment across multiple natural hazards to make informed decisions and comply with SEC climate disclosure rules.

###  Solution

Production-grade data pipeline integrating real-time data from USGS (earthquakes), NASA FIRMS (wildfires), and NOAA (weather alerts) to calculate composite risk scores. 

###  Business Value

- **Multi-source government API integration** with error handling
- **Geographic risk scoring algorithm** with configurable weights
- **RESTful API with FastAPI** (6 endpoints)
- **Interactive Streamlit dashboard** with real-time visualizations
- **Production-grade error handling and retry logic**

###  Key Metrics

- **API Response Time:** <2 seconds for single location analysis
- **Data Sources:** 3 government APIs integrated
- **Risk Factors:** 5 hazard types assessed
- **Dashboard Load Time:** <3 seconds
- **Data Freshness:** Real-time (as current as government sources)

###  Features

- **Data Engineering:** Multi-source data integration, schema validation, error handling
- **API Development:** RESTful design, FastAPI, Pydantic models
- **Data Science:** Risk scoring algorithms, geographic analysis, statistical modeling
- **Visualization:** Plotly charts, interactive dashboards, Streamlit
- **Production Patterns:** Retry logic, connection pooling, monitoring


##  Algorithm Architecture

### Composite Risk Calculation:

- Weighted multi-hazard scoring system combining 5 disaster types
- Default weights: Wildfire (30%), Earthquake (25%), Weather (20%), Flood (15%), Heat (10%)
- Configurable weight parameters for custom risk profiles
- Scores normalized to 0-100 scale with risk level classification (Low/Moderate/High/Extreme)

### Individual Hazard Scoring:

- **Earthquake Risk:** Historical frequency × magnitude severity × proximity decay

  - **Frequency score:** Event count normalized to 50+ events = max risk
  - **Magnitude score:** Max magnitude normalized to 7.0+ = max risk
  - **Weighted combination:** 60% frequency + 40% magnitude

- **Wildfire Risk:** Active fire detections × intensity × distance decay

  - **Frequency score:** Fire count normalized to 20+ fires = max risk
  - **Intensity score:** Fire Radiative Power normalized to 500 MW = max risk
  - **Proximity score:** Distance-based decay function
  - **Weighted combination:** 40% frequency + 30% intensity + 30% proximity

- **Weather Risk:** NOAA alert severity mapping

  - **Extreme alerts** = 100, **Severe** = 75, **Moderate** = 50, **Minor** = 25

### Geographic Processing:

- Haversine distance calculation for accurate geographic proximity
- Configurable search radius (default: 500km for earthquakes, 100km for wildfires)
- Time-based filtering (365 days for seismic, 30 days for fires)

### Data Quality & Validation:

- Schema validation for inconsistent government API responses
- Null handling and data completeness checks
- Outlier detection and normalization

### Performance Optimization:

- Vectorized NumPy operations for distance calculations
- Pandas-based data processing for efficiency
- Cached connector instances for reduced API calls

###  Data Sources

- **USGS**: Earthquake data (earthquake.usgs.gov)
- **NASA FIRMS**: Wildfire data (firms.modaps.eosdis.nasa.gov)
- **NOAA**: Weather alerts (api.weather.gov)


##  Project Structure
```
disaster-risk-platform/
├── src/
│   ├── api_connectors/      # Data ingestion from government APIs
│   ├── risk_scoring/        # Risk calculation algorithms
│   └── utils/               # Helper functions
├── api/                     # FastAPI endpoints
├── dashboard/               # Streamlit dashboard
├── data/                    # Data storage
└── tests/                   # Unit tests
```

###  Key Files

- `src/api_connectors/` - Data ingestion from government APIs
- `src/risk_scoring/` - Risk calculation algorithms
- `api/main.py` - FastAPI REST endpoints
- `dashboard/app.py` - Streamlit interactive dashboard


##  Quick Start

### 1. Setup
```bash
# Close repository
git clone https://github.com/michael-gurule/disaster-risk-platform.git
cd disaster-risk-platform

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Test connectors
python src/api_connectors/usgs_connector.py
python src/api_connectors/nasa_firms_connector.py
python src/api_connectors/noaa_weather_connector.py

# Run API
python api/main.py
# Visit http://localhost:8000/docs

# Run Dashboard
streamlit run dashboard/app.py
# Visit http://localhost:8501
```

###  Dashboard Features:
- Interactive location search
- Real-time data fetching
- Risk score visualizations
- Multi-tab detailed analysis
- Quick location presets

### Future Improvements

- [ ] FEMA flood zone integration
- [ ] Historical risk trends
- [ ] Email/Slack alerting
- [ ] PostgreSQL database
- [ ] Docker containerization
- [ ] AWS deployment

---

##  Dashboard

<p align="center">
<img width="1463" height="723" alt="Screenshot 2025-12-16 at 8 36 43 PM" src="https://github.com/user-attachments/assets/b569ea22-6901-4921-840b-e8e30dc2523d" />
Dashboard overview showing composite risk score
</p> 
<br>

<p align="center">
<img width="1168" height="570" alt="Screenshot 2025-12-16 at 8 37 56 PM" src="https://github.com/user-attachments/assets/9f60a12a-80b3-49bf-a89d-6d549dcfe0d2" />
 Earthquake data visualization
</p> 
<br>
  
<p align="center">
<img width="1175" height="682" alt="Screenshot 2025-12-16 at 8 38 17 PM" src="https://github.com/user-attachments/assets/17f7d1c7-334b-4b27-95df-f75438e3683e" />
Wildfire detection map
</p> 
<br>

<p align="center">
<img width="1477" height="782" alt="Screenshot 2025-12-16 at 8 38 55 PM" src="https://github.com/user-attachments/assets/730aafa6-eead-4569-957f-1ae70529de2b" /> 
Weather alerts display
</p> 
<br>

<p align="center">
<img width="1489" height="819" alt="Screenshot 2025-12-16 at 8 35 09 PM" src="https://github.com/user-attachments/assets/1da90e08-2a96-4cd8-bf34-61938b87fd0e" />
API interactive documentation
</p> 
<br>

---
##  License

MIT License

## Contributing

This is a portfolio project. For questions or collaboration:

**Michael Gurule**

- [![Email Me](https://img.shields.io/badge/EMAIL-8A2BE2)](michaelgurule1164@gmail.com)
- [![LinkedIn](https://custom-icon-badges.demolab.com/badge/LinkedIn-0A66C2?logo=linkedin-white&logoColor=fff)](www.linkedin.com/in/michael-j-gurule-447aa2134)
- [![Medium](https://img.shields.io/badge/Medium-%23000000.svg?logo=medium&logoColor=white)](https://medium.com/@michaelgurule1164)

---

<p align="center">
  <img src="https://github.com/user-attachments/assets/d1d1a864-0669-41d9-afbe-c54a98d16707" alt="CONSTELLATION" width="40">
  <br>
  <sub>Built by Michael Gurule | Data: NASA USGS NOAA (Public)</sub>
</p>
