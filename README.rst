===========================================
european_weather_elt: Weather Data Pipeline
===========================================

An ELT (Extract-Load-Transform) pipeline that retrieves historical daily temperature data from the Open-Meteo API, loads it into a DuckDB database, and optionally exports it to a `.parquet` file for analysis in tools like Power BI.

This project is ideal for climate analysts, researchers, and data scientists investigating weather trends across Europe and comparing recent years with past decades.

-------------------
🌟 Project Features
-------------------

- Extracts weather data (min/max temperatures) using city name and year
- Automatically geocodes cities using Open-Meteo's geocoding API
- Loads data into DuckDB
- Exports all collected data as a Parquet file for analysis
- CLI-powered: simple and scriptable
- Minimal setup required

----------------------
📦 Installation & Setup
----------------------

This project uses [`uv`](https://github.com/astral-sh/uv) for managing Python dependencies.

1. **Install `uv` (only once):**

   .. code-block:: bash

      pip install uv

2. **Create a virtual environment:**

   .. code-block:: bash

      uv venv

3. **Activate the virtual environment:**

   .. code-block:: bash

      # On Windows:

      .venv\Scripts\activate

      # On macOS/Linux:

      source .venv/bin/activate

4. **Install dependencies from `pyproject.toml`:**

   .. code-block:: bash

      uv pip install -r pyproject.toml

-------------------------------
🛠 How to Run the Data Pipeline
-------------------------------

Use the CLI to extract weather data for any European city and year.

**Extract + Load (to DB):**

.. code-block:: bash

   python . <city> <year>

Example:

.. code-block:: bash

   python . Lisbon 2024

This:

- Geocodes the city
- Extracts daily weather data for all months in that year
- Loads the results into `data/weather.duckdb`

If data for that city/year already exists in the database, it will be skipped.

-------------------------------
📤 Exporting Data to Parquet
-------------------------------

Once you’ve collected data for all the cities and years you want:

.. code-block:: bash

   python . export

This exports all contents of the DuckDB database to:

data/export/weather.parquet


You can now load this file directly into Power BI or any other analysis tool that supports Parquet format.

------------------------------
📈 Exploratory Data Analysis (EDA) in Python
------------------------------

Before building the dashboard, we explored the data using Python and Jupyter Notebooks to validate trends and identify key insights.

The following visualizations were generated and saved in the `viz/charts/` folder:

- **`ave_max_temp.png`** – Average maximum temperatures across all cities and years
- **`ave_min_temp.png`** – Average minimum temperatures by year and region
- **`temp_per_city.png`** – City-by-city comparison of average temperature changes
- **`heatmap.png`** – Yearly heatmap showing temperature gradients by city

These revealed:

- A **clear upward trend** in temperatures across all five cities studied
- **Rome** and **Paris** showed the most pronounced increases in maximum temperatures
- **Stockholm** displayed steady warming of minimum temperatures, indicating milder winters
- Signs of **temperature convergence**, with traditionally colder cities warming faster

------------------------------
📊 Power BI Dashboard Insights
------------------------------

We built a Power BI report (`viz/European_Weather_Report.pbix`) to present average max temperature trends more interactively.

Included visuals:

- **Line Chart**: `ave_temp_max` over time by city
- **Map Visualization**: Pinpoints each city’s location
- **Insight Summary**: Narrative card for interpretation
- **Matrix Table**: Displays `ave_temp_max` by city and year

**Notable Insight:**

> Between **2008 and 2024**, average maximum temperatures surged most sharply — particularly in **Rome**, where values rose by ~2.3°C since 1984.  
> Meanwhile, **Stockholm** shows warming winters — a sign of **polar amplification**.

#### Implications:

- **Public Health**: Nighttime warming may increase heat stress in cities like Paris and Warsaw.
- **Urban Planning**: Infrastructure must adapt to extreme heat, especially in Southern and Central Europe.
- **Policy-Making**: These historical patterns can support stronger climate action and localized emission reduction efforts.

📁 The full dashboard is available here:

- `viz/European_Weather_Report.pbix`

-------------------
📝 License & Credits
-------------------

- License: MIT
- Created with `Cookiecutter` and the `audreyr/cookiecutter-pypackage` template

.. _Cookiecutter: https://github.com/audreyr/cookiecutter
.. _`audreyr/cookiecutter-pypackage`: https://github.com/audreyr/cookiecutter-pypackage
