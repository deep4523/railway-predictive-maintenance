import pandas as pd
import matplotlib.pyplot as plt

# Step 1: Load CSV file
df = pd.read_csv("railway_data.csv")

# Step 2: Function to check status
def check_status(temp, vib):
    if temp > 75 or vib > 5:
        return "High Risk"
    else:
        return "Normal"

# Step 3: Apply function
df["Status"] = df.apply(lambda x: check_status(x["Temperature"], x["Vibration"]), axis=1)

# Step 4: Print full data
print("\n--- Railway Maintenance Data ---\n")
print(df)

# Step 5: Alert system
print("\n--- ALERTS ---\n")
for index, row in df.iterrows():
    if row["Status"] == "High Risk":
        print(f"⚠️ Alert at Row {index}: Temp={row['Temperature']} | Vibration={row['Vibration']}")

# Step 6: Graph visualization
plt.figure()

# Scatter plot
for status in ["Normal", "High Risk"]:
    subset = df[df["Status"] == status]
    plt.scatter(subset["Temperature"], subset["Vibration"], label=status)

plt.xlabel("Temperature")
plt.ylabel("Vibration")
plt.title("Railway Predictive Maintenance System")
plt.legend()
plt.grid()

plt.show()
