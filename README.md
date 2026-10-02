# Bangalore House Price Predictor

A Flask web app that predicts house prices in Bangalore using a Ridge Regression model trained on the Bengaluru housing dataset.

## Project Structure

```
├── archive/
│   └── Bengaluru_House_Data.csv   # Raw dataset
├── Cleaned_data.csv                # Cleaned dataset (outliers removed, nulls handled)
├── house_prediction.ipynb          # EDA, cleaning, feature engineering, model training
├── RidgeModel.pkl                  # Trained Ridge Regression model (pickled)
├── main.py                         # Flask app — serves UI and /predict endpoint
└── templates/
    └── index.html                  # Frontend form
```

## How It Works

1. `house_prediction.ipynb` cleans the raw data and trains a Ridge Regression model on `location`, `total_sqft`, `bath`, and `bhk` to predict price.
2. The trained model is saved as `RidgeModel.pkl`.
3. `main.py` loads the model and cleaned data, and serves:
   - `/` — renders the form, with the location dropdown populated from the dataset
   - `/predict` — accepts form data (POST), builds a single-row DataFrame, runs the model, returns the predicted price
4. `index.html` is a Bootstrap form. On submit, it sends the form data via `XMLHttpRequest` to `/predict` without reloading the page, and injects the returned price into the page.

## Tech Stack

- **ML**: pandas, NumPy, scikit-learn (Ridge Regression)
- **Backend**: Flask
- **Frontend**: HTML, Bootstrap 4, vanilla JS (XHR)

## Setup

```bash
pip install flask pandas numpy scikit-learn
python main.py
```

App runs at `http://localhost:5001`

## Input Features

| Feature | Type |
|---|---|
| Location | Dropdown (from dataset) |
| BHK | Number |
| Bathrooms | Number |
| Total Sqft | Number |

## Output

Predicted price in ₹ (Lakhs), scaled by 1e5 in `main.py`.

## Known Limitations

- No input validation on the frontend/backend — non-numeric or empty fields will error
- Paths to `Cleaned_data.csv` and `RidgeModel.pkl` are relative, so the app must be run from the project root
