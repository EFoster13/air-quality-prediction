# Data Collection Strategy

## Historical Data Collection (One-Time)
**Goal:** Collect 12 months of hourly data for all 3 cities

**Timeline:**
- Date range: January 1, 2024 - December 31, 2024
- Granularity: Hourly readings
- Expected records: 3 cities × 365 days × 24 hours = ~26,280 records

**API Usage:**
- Historical endpoint requires Unix timestamps
- January 1, 2024 00:00 UTC = 1704067200
- December 31, 2024 23:59 UTC = 1735689540
- Strategy: Collect 1 month at a time per city to avoid rate limits

**Data to collect per record:**
- Timestamp
- All pollutants (PM2.5, PM10, NO2, O3, CO, SO2)
- Weather conditions (temp, humidity, wind, pressure)
- City identifier

## Ongoing Data Collection (Daily)
**Goal:** Collect fresh data daily for validation and continued learning

**Schedule:** Run script daily at around 12:00 PM local time
**Process:**
1. Fetch current pollution for all 3 cities
2. Fetch current weather for all 3 cities  
3. Store in database
4. Verify data quality
5. Log any errors

**API calls per day:** 3 cities × 2 calls = 6 calls/day (well within 1000/day limit)

## Data Validation Checks
After each collection:
- Verify timestamps are sequential
- Check for null values (acceptable: <5%)
- Validate ranges (PM2.5: 0-500, temp: -50 to 130°F)
- Confirm no duplicate timestamps per city
- Log collection success rate

## Backup Strategy
- Save raw JSON responses to `data/raw/YYYY-MM-DD_city.json`
- Keep raw data for 30 days
- Database is primary storage
- Weekly database backups


