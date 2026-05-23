import matplotlib
matplotlib.use("Agg")   

import matplotlib.pyplot as plt
import pandas as pd
from geopy.geocoders import Nominatim


geolocator = Nominatim(user_agent="nv_mapper")

*Newly added try to see if the definition works if not remove.*
df = pd.DataFrame({
    "place": ["Las Vegas, NV", "Nelson, NV", "Rockland, NV"],
    "color": ["blue", "orange", "red"]
})

df["location"] = df["place"].apply(geolocator.geocode)
df["lat"] = df["location"].apply(lambda loc: loc.latitude if loc else None)
df["lon"] = df["location"].apply(lambda loc: loc.longitude if loc else None)


print("\nGeocoded Coordinates:")
for _, row in df.iterrows():
    print(f"{row['place']}: lat={row['lat']}, lon={row['lon']}")
    
ax.add_feature(cfeature.LAND, facecolor="lightgray")
ax.add_feature(cfeature.OCEAN, facecolor="lightblue")
ax.add_feature(cfeature.LAKES, facecolor="white")
ax.add_feature(cfeature.RIVERS, edgecolor="blue")
ax.add_feature(cfeature.BORDERS, edgecolor="black")
ax.add_feature(cfeature.STATES, edgecolor="gray")

plt.figure(figsize=(10, 6))
plt.scatter(df["lon"], df["lat"], color="blue", s=80)
plt.title("Geopy Locations in Nevada")
plt.xlabel("Longitude")
plt.ylabel("Latitude")


plt.savefig("geopy1.png", dpi=200, bbox_inches="tight")
