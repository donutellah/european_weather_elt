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

-----------------------
📊 Insights & Analysis
-----------------------

We analyzed average daily temperatures across five major European cities — **Paris, Rome, Vienna, Warsaw, and Stockholm** — over select years spanning from **1984 to 2024**, using Power BI for visualization. The data reveals a **clear, decade-over-decade increase in average maximum temperatures**, with the most significant rise occurring **between 2008 and 2024**.

- For example, **Rome's average max temperature in 2024 is ~2.3°C higher than in 1985**, a substantial increase that aligns with Mediterranean heatwave patterns.
- **Stockholm**, while generally cooler, shows a consistent upward trend in minimum temperatures, suggesting **less cold nights and warmer winters** in Northern Europe — a classic signal of **polar amplification**.

These patterns provide quantitative backing to the broader climate narrative:

> "Europe is warming faster than the global average, and urban areas are at the frontlines."

📌 **Implications:**

- **Public health**: Rising nighttime temperatures (especially in Paris and Warsaw) could intensify heat stress and reduce nighttime recovery — a concern for vulnerable populations.
- **Urban planning**: Cities may need to invest in heat-resilient infrastructure, particularly in southern and central Europe.
- **Policy-making**: Local governments can use these findings to push for aggressive emissions reduction targets, especially where warming is most pronounced.

🖥️ **Power BI Dashboard Includes:**

- City-by-city temperature trend lines
- Yearly comparison bar charts
- Heatmaps of temperature patterns
- Interactable filters by city and year

You can find the final Power BI report here:

📁 `viz/European_Weather_Report.pbix`


-------------------
📝 License & Credits
-------------------

- License: MIT
- Created with `Cookiecutter` and the `audreyr/cookiecutter-pypackage` template

.. _Cookiecutter: https://github.com/audreyr/cookiecutter
.. _`audreyr/cookiecutter-pypackage`: https://github.com/audreyr/cookiecutter-pypackage
