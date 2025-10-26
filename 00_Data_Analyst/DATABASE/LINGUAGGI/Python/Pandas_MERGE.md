funzione simile a join da fare in pandas


air_quality = pd.merge(air_quality, stations_coord, how="left", on="location")
air_quality.head()