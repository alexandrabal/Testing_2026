import pandas as pd

adjust = pd.read_csv("/content/sample_data/Adjust raw data - Adjust raw data.csv")
meta = pd.read_csv("/content/sample_data/Meta raw data.csv")

for name, df in [("ADJUST", adjust), ("META", meta)]:
    print("=" * 40, name, "=" * 40)
    print("rows, columns:", df.shape)
    print("\ncolumns and types:")
    print(df.dtypes)
    print("\nfirst 5 rows:")
    print(df.head())
    print("\nmissing values per column:")
    print(df.isna().sum())
    print("\nzeros and non-numeric values in metric columns:")
    metric_cols = [c for c in ["spend", "impressions", "clicks", "installs", "purchases",
                               "purchase_revenue", "d0_purchase_revenue", "d30_purchase_revenue"]
                   if c in df.columns]
    rows = []
    for c in metric_cols:
        nums = pd.to_numeric(df[c].astype(str).str.strip('"').str.replace(",", "", regex=False),
                             errors="coerce")
        rows.append({"column": c,
                     "zeros": int((nums == 0).sum()),
                     "zero_%": round(100 * (nums == 0).mean(), 2),
                     "not_numeric": int(nums.isna().sum()),
                     "total": round(nums.sum(), 2)})
    print(pd.DataFrame(rows).to_string(index=False))
    print("\nunique values per column:")
    print(df.nunique())
    print("\nexact duplicate rows:", df.duplicated().sum())
    print("\ndate range:", df["date"].min(), "to", df["date"].max())
    print("\ncountries:")
    print(df["country"].value_counts(dropna=False).head(10))
