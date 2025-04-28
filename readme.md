# Buffalo Crime Analysis Dashboard

## Project Overview

This project analyzes and predicts crime patterns in Buffalo using various approaches, including crime risk prediction, crime forecasting, threat score assessments, and neighborhood crime trend analysis.

## Folder Structure

- **data/**: Contains all data files used in the project.
  - `data/forecast/`: Forecasting-related data.
  - `data/processed/`: Processed data files.
  - `data/raw/`: Raw crime data.
  - `data/risk/`: Data related to risk analysis.
  - `data/threat/`: Data related to threat score calculations.
  - `data/trends/`: Data related to neighborhood crime trends.

- **db/**: Contains the database used in the project.
  - `db/incidents.db`: SQLite database with crime data.

- **exp/**: Contains all Jupyter notebooks for analysis and experiments.
  - `exp/forecast.ipynb`: Crime forecasting notebook.
  - `exp/risk.ipynb`: Crime risk prediction notebook.
  - `exp/threat.ipynb`: Threat score assessment notebook.
  - `exp/trends.ipynb`: Neighborhood crime trends notebook.

- **scripts/**: Contains Python scripts for data preparation and processing.
  - `scripts/__pycache__/`: Compiled Python files.
  - `scripts/__init__.py`: Initialization file for the script folder.
  - `scripts/create_database.py`: Script to create the database.
  - `scripts/data_preperation.py`: Data preparation script.

- **app.py**: Streamlit application for presenting the crime analysis dashboard.
- **project_report_phase_3.pdf**: Project report describing technical and functional details.

## Building and Running the App

To build and run the application from source code, follow these steps:

1. **Set Up the Environment**

    Ensure you have Python 3.11 or a compatible version installed. Install the required dependencies:

    ```bash
    pip install -r requirements.txt
    ```

2. **Prepare the Data**

    Run the data preparation script to set up the necessary database and data:

    ```bash
    python scripts/create_database.py
    ```

3. **Execute Jupyter Notebooks**

    Open and run all cells in each of the following notebooks:
    - `exp/forecast.ipynb`
    - `exp/risk.ipynb`
    - `exp/threat.ipynb`
    - `exp/trends.ipynb`

4. **Run the Streamlit App**

    Launch the Streamlit application:

    ```bash
    streamlit run app.py
    ```

5. **Access the Dashboard**

    The crime data analysis dashboard will be available in your browser, allowing you to view and explore the results of the analysis, including crime trends, forecasting, and risk predictions.

---

# Highlights

## 1. Real-Time Crime Risk Prediction

- **Functionality**: Predicts the highest risk day and hour for crimes using historical crime data.
- **Tools Used**: Random Forest Classifier, integrated with Streamlit for real-time predictions.
- **How It Works**: The user selects a neighborhood, day of the week, and hour to predict the crime risk. The system predicts crime risk and displays the results via a heatmap visualization.
- **Visualization**: 
    ```python
    st.write("Heatmap visualization of crime risk.")
    st.map(heatmap_data)
    ```
- **Location in Code**: Implemented in `real_time_risk_prediction()` inside `app.py`.

## 2. Crime Forecasting Using Facebook Prophet Model

- **Functionality**: Forecasts crime trends over time, identifying potential crime surges in Buffalo neighborhoods.
- **Tools Used**: Facebook Prophet model for time-series forecasting.
- **How It Works**: Forecasts crime trends for the upcoming year based on historical data, both city-wide and by neighborhood. Visualizes the forecasted crime data as a line chart.
- **Visualization**:
    ```python
    fig = go.Figure()
    fig.add_trace(go.Scatter(x=forecast_data['ds'], y=forecast_data['yhat'], mode='lines'))
    st.plotly_chart(fig)
    ```
- **Location in Code**: Implemented in `crime_forecasting()` inside `app.py`.

## 3. Threat Score Assessment

- **Functionality**: Predicts the safety level (threat score) for specific areas and times based on historical crime data.
- **Tools Used**: XGBoost Regressor for threat score prediction, Streamlit for user interface.
- **How It Works**: The user selects a neighborhood, day of the week, and hour of the day. The system predicts a threat score and categorizes it into low, moderate, or high risk.
- **Visualization**:
    ```python
    threat_score = model.predict(encoded_input)
    fig = go.Figure(go.Indicator(mode="gauge+number", value=threat_score, title={"text": "Threat Score"}, gauge={...}))
    st.plotly_chart(fig)
    ```
- **Location in Code**: Implemented in `threat_assessment()` inside `app.py`.

## 4. Neighborhood Crime Trends and Forecasting

- **Functionality**: Analyzes and forecasts neighborhood crime trends, helping authorities understand where specific crimes are more likely to occur.
- **Tools Used**: Support Vector Machine (SVM) classifiers, Plotly for data visualization.
- **How It Works**: The app predicts the likelihood of various crime types in a given neighborhood based on temporal features.
- **Visualization**:
    ```python
    fig = go.Figure(go.Scattermapbox(lat=crime_data['lat'], lon=crime_data['lon'], mode='markers', marker=go.scattermapbox.Marker(size=9)))
    st.plotly_chart(fig)
    ```
- **Location in Code**: Implemented in `neighborhood_crime_analysis()` inside `app.py`.

## 5. 3D Crime Map Visualization in Web Interface

- **Functionality**: Provides an immersive, interactive map for visualizing crime data across Buffalo, highlighting crime hotspots and trends.
- **Tools Used**: Plotly and Pydeck for advanced map visualizations.
- **How It Works**: The 3D map displays individual crime incidents and crime density using a Hexagon Layer. Dark red indicates high crime intensity, light yellow indicates low density. Interactive scatterplots provide details about incidents.
- **Visualization**:
    ```python
    fig = go.Figure(go.Scattermapbox(lat=crime_data['lat'], lon=crime_data['lon'], mode='markers', marker=go.scattermapbox.Marker(size=9)))
    st.plotly_chart(fig)
    ```
- **Location in Code**: Implemented in 3D crime mapping section inside `app.py`.

## 6. Data Management and Integration

- **Functionality**: Manages crime data stored in an SQLite database and integrates it into the app for analysis and visualization.
- **Tools Used**: SQLite, Pandas for data manipulation, Joblib for model loading.
- **How It Works**: The database stores historical crime data, which is fetched and processed for analysis. Machine learning models are loaded via Joblib to make real-time predictions.
- **Data Fetch Example**:
    ```python
    connection = sqlite3.connect('db/incidents.db')
    cursor = connection.cursor()
    ```
- **Location in Code**: Data management handled by helper functions in `app.py`.

## 7. Web Interface for Real-Time Interaction

- **Functionality**: Allows users (law enforcement, city planners) to interact with the crime prediction and analysis models in real-time.
- **Tools Used**: Streamlit for web app development.
- **How It Works**: Users input parameters like neighborhood, crime type, and time to see real-time predictions and forecasts.
- **Visualization**:
    ```python
    fig = px.pie(crime_data, names='crime_type', title='Crime Type Distribution')
    st.plotly_chart(fig)

    fig = px.bar(crime_data, x='day_of_week', y='crime_count', title='Crime Distribution by Day')
    st.plotly_chart(fig)
    ```
- **Location in Code**: Implemented across various user input and visualization sections inside `app.py`.

---

## Data Source

- Buffalo Open Data Portal: [https://data.buffalony.gov/](https://data.buffalony.gov/)

---

## License

This project is open-sourced under the MIT License.

---
