# Retail Store Optimization

A Python-based group project that analyzes retail category sales and recommends inventory levels under budget and shelf-space constraints. The project is provided as a Jupyter Notebook (`.ipynb`) and uses a reproducible synthetic dataset so it can be run without private store data.

## Project Objectives

- Explore weekly sales and demand patterns across retail categories.
- Estimate average demand and demand variability.
- Calculate safety stock and reorder points using a target service level.
- Allocate inventory across categories to maximize expected gross profit while respecting purchasing-budget and shelf-capacity limits.
- Compare the optimized inventory plan with a simple one-week-demand baseline.

## Project Files

- `Retail_Store_Optimization_Group_Project.ipynb` — main notebook containing the dataset, analysis, optimization model, charts, and conclusion prompts.
- `README.md` — project overview and instructions.

## Requirements

- Python 3.9 or newer recommended
- Jupyter Notebook or JupyterLab, or Google Colab
- Packages:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `scipy`

## Setup

### Option A: Run locally

1. Install Python.
2. Download or clone the project files and open a terminal in the project folder.
3. (Recommended) Create and activate a virtual environment:

   **Windows**
   ```bash
   python -m venv .venv
   .venv\\Scripts\\activate
   ```

   **macOS / Linux**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

4. Install the required packages:

   ```bash
   python -m pip install numpy pandas matplotlib scipy notebook
   ```

5. Launch Jupyter:

   ```bash
   jupyter notebook
   ```

6. Open `Retail_Store_Optimization_Group_Project.ipynb` and run the cells from top to bottom.

### Option B: Run in Google Colab

1. Open Google Colab.
2. Upload `Retail_Store_Optimization_Group_Project.ipynb`.
3. Run the notebook cells from top to bottom. If Colab asks to install a missing package, install it with `!pip install package-name`.

## How the Program Works

1. **Sample data generation:** creates 26 weeks of weekly unit sales for 12 retail categories, along with sample selling prices, unit costs, and shelf-space requirements.
2. **Exploratory analysis:** charts weekly units sold and calculates category-level demand and margin metrics.
3. **Inventory policy:** estimates safety stock and reorder points using a 95% target service level and a one-week lead-time assumption.
4. **Optimization:** uses `scipy.optimize.linprog` to choose category stock quantities that maximize estimated gross profit subject to the inventory budget, shelf capacity, and per-category stock bounds.
5. **Evaluation:** compares the optimized stock allocation with a baseline of approximately one week of average demand and displays allocation charts.

## Configuration

In the optimization section of the notebook, you can change:

- `INVENTORY_BUDGET` — total available purchasing budget.
- `SHELF_CAPACITY` — total available shelf-space units.
- `SERVICE_LEVEL_Z` — z-score used for safety-stock calculation.
- `LEAD_TIME_WEEKS` — assumed replenishment lead time.

The notebook also sets category-specific minimum and maximum stock bounds. Adjust these to reflect your store's policies and practical constraints.

## Using Real Store Data

The notebook currently generates synthetic data for demonstration. To use your team's data:

1. Prepare a CSV with these columns:
   - `week` — date or week identifier
   - `category` — retail category name
   - `units_sold` — units sold in that week
2. Replace the synthetic sales-data creation cell with:

   ```python
   sales = pd.read_csv("your_retail_sales.csv", parse_dates=["week"])
   ```
3. Update the category information table (`base`) with your categories, average demand inputs (if used), selling prices, unit costs, and shelf-space requirements.
4. Ensure category names match between the sales file and the category information table.
5. Re-run the notebook and review the outputs.

For a more realistic analysis, consider adding on-hand inventory, stockout history, supplier lead times, pack sizes, promotions, expiry dates, and store-level shelf dimensions.

## Key Assumptions and Limitations

- The sample data is simulated and should not be treated as actual store performance.
- The analysis is performed at category level rather than SKU level.
- Demand is approximated using historical average and standard deviation; the safety-stock calculation assumes a normal-demand approximation.
- The optimization is a simplified allocation model. It does not explicitly model stockouts, lost sales, product substitution, replenishment timing, perishability, or integer-programming effects.
- Validate the recommendations with real operational data before using them for purchasing decisions.

## Group Project Presentation Suggestions

Include:
1. The retail inventory problem and why it matters.
2. Data fields and assumptions.
3. Sales and demand charts.
4. Safety-stock and reorder-point method.
5. Optimization objective and constraints.
6. Baseline versus optimized results.
7. Limitations and possible future improvements.

## License

This project is intended for educational and group-project use. Add a license if you plan to distribute or reuse it beyond your course.
