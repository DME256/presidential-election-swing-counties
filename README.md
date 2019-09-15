# presidential-election-swing-counties
The features of this map is to identify, by voter counts, the top 100 counties that did not register a majority for the same party in the 2012 and 2016 Presidential Election. And also represent the 100 highest populated counties that did vote the same for each party, GOP and DEM. Upon loading the map you will see the top 100 "Swing Counties" in graduated shades of green by voters. The top 100 counties that voted for the Democratic candidate in both elections in blue,the top 100 counties that voted for the Republican candidate in both elections in red. Click on each swing county for voter total for the 2016 and 2012 elections. For the red and blue counties the 2016 election vote totals are displayed. 
The purpose was to identify if resources could be used in the identified swing counties to influence voters in the respective counties. And likewise perhaps not devote resources to counties that historically are strong holds for each party. 
# How the map was created
The data for 2012 and 2012 elections and then sorted by number of voters and then whether or not the county voted REP, DEM or split in the past two elections. The results were then placed into 3 seperate datasets.
the SQL used for maps:

    SELECT 
    dme256.cb_2015_us_county_20m.cartodb_id,
    dme256.cb_2015_us_county_20m.the_geom,
    statefp,
    countyfp,
    countyns,
    affgeoid,
   	county_name,
    lsad,
    aland,
	awater,
    votes_dem_2016,
    votes_gop_2016,
    total_votes_2016,
    per_dem_2016,
    per_gop_2016,
    diff_2016
    
    From dme256.us_county_level_presidential_results_2016, dme256.cb_2015_us_county_20m
    Where fips = geoid

    SELECT 
	dme256.cb_2015_us_county_20m_1.the_geom_webmercator,
   	dme256.cb_2015_us_county_20m_1.cartodb_id,
    dme256.cb_2015_us_county_20m_1.the_geom,
    statefp,
    countyfp,
    countyns,
    affgeoid,
   	name,
    lsad,
    aland,
	awater,
    red_total_2016,
    red_dem_2016,
    red_gop_2016
  
From dme256.red_county, dme256.cb_2015_us_county_20m_1
Where red_fips_code = geoid

SELECT 
	dme256.cb_2015_us_county_20m_2.the_geom_webmercator,
   	dme256.cb_2015_us_county_20m_2.cartodb_id,
    dme256.cb_2015_us_county_20m_2.the_geom,
    statefp,
    countyfp,
    countyns,
    affgeoid,
   	county_name,
    lsad,
    aland,
	awater,
    blue_total_2016,
    blue_dem_2016,
    blue_gop_2016
    
    
From dme256.blue_counties, dme256.cb_2015_us_county_20m_2
Where blue_fips_code = geoid

The swing counties are represented in 5 quantiles by total GOP/DEM voters.