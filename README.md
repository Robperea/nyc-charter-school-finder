# Charter School Finder

An interactive map of public charter schools in New York City. Success Academy schools are highlighted. You can search by name, filter by borough, show Success Academy only, or sort schools by distance from you.

**Live map:** _add your GitHub Pages link here after publishing_

## Scope
Operating public charter schools in the five boroughs that appear in the official NYSED directory **and** have a location in the NCES 2024-25 school locations file. Each school is placed at its primary address, so this is **not** every campus or satellite site.

## Numbers at a glance
| | Count |
|---|---|
| NYC charter schools in the NYSED directory (as of Sept 2, 2025) | 299 |
| On the map (matched to an NCES location) | 281 |
| Not on the map yet (opened 2025 or later, no location in the NCES 2024-25 file) | 18 |
| Buildings on the map | 263 (16 contain more than one school) |
| Success Academy schools on the map | 38 |

## Sources
Both data files were downloaded on October 29, 2026.
1. **NYS Charter School Directory, 2025-2026**, New York State Education Department ([directory page](https://www.nysed.gov/charter-schools/charter-schools-directory); Excel dated "as of 09-02-2025"). The official list of charter schools: name, county, year opened, authorizer, NYSED institution ID. Filtered to Region = New York City.
2. **Public School Locations 2024-25**, NCES EDGE ([dataset page](https://data-nces.opendata.arcgis.com/datasets/nces::public-school-locations-2024-25); CSV published January 29, 2026). Source of street address and latitude/longitude. It covers every US public school and has no charter flag, so it cannot identify charters by itself.
3. **State of the NYC Charter School Sector**, NYC Charter School Center ([page](https://nyccharterschools.org/state-of-the-nyc-charter-school-sector/)). Reference figures only (285 charter schools across about 420 campuses in 2025-26). Not used to build the map.
4. **NYC DOE school page for Success Academy Charter School - Bronx 5 Upper** ([page](https://pws.nycenet.edu/schools/X638)). Used once, to verify an address (see Handling discrepancies).

## How current is the data
- The NYSED directory is dated September 2, 2025 and covers the 2025-26 school year.
- The NCES locations are from the 2024-25 school year.
- This map was built in October 2026, during the 2026-27 school year. Openings, closures and moves since those snapshots are not reflected, apart from schools the directory already listed as opening in 2026.

## Method
1. From the NCES file, kept New York State rows in the five NYC counties (New York, Kings, Bronx, Queens, Richmond).
2. Identified charter schools: NYC district schools share one of 33 district-level IDs, while each charter school has its own. Everything outside those 33 was a charter candidate, minus two state psychiatric facilities.
3. Matched each candidate to the NYSED directory by normalized school name (fuzzy match, threshold 0.9), plus 8 manual matches for renamed or abbreviated schools.
4. Grouped schools into buildings: same normalized street address and ZIP, or within about 20 meters of each other.
5. Marked Success Academy schools by name.

## Reconciliation and known gaps
- **18 NYSED schools are not on the map.** 17 of them list a 2025 or 2026 opening year, after the NCES 2024-25 snapshot. They need geocoded addresses from another source:

| School | County | Opened | Authorizer |
|---|---|---|---|
| Haven Charter High School | Bronx | 2025 | SUNY |
| Lamad Averne Academy Charter School | Bronx | 2025 | SUNY |
| Next Generation Charter School | Bronx | 2026 | SUNY |
| South Bronx Classical Charter School V | Bronx | 2025 | SUNY |
| South Bronx Classical Charter School VI | Bronx | 2025 | Regents |
| Success Academy Charter School - NYC 17 | Bronx | 2026 | SUNY |
| Success Academy Charter School - NYC 18 | Bronx | 2026 | SUNY |
| Achievement First Charter School 11 | Kings | 2025 | SUNY |
| Explore Enrich Charter School | Kings | 2025 | SUNY |
| Kwenda Collegiate Girls Charter School | Kings | 2025 | SUNY |
| Math, Engineering, and Science Academy Charter High School 2 | Kings | 2025 | SUNY |
| Success Academy Charter School – NYC 15 | Kings | 2025 | SUNY |
| Uncommon New York City Charter School #1 | Kings | 2025 | SUNY |
| Urban Dove Team Charter School V | Kings | 2025 | SUNY |
| American Dream Charter School II | New York | 2025 | Regents |
| Zeta Charter School - Queens 2 | Queens | 2025 | SUNY |
| Zeta Charter School - Queens Elmhurst | Queens | 2025 | SUNY |
| Zeta Charter School - Queens Jamaica | Queens | 2025 | SUNY |

- **1 NCES school was left out:** Choice Charter School (423 E 138th St, Bronx) appears in NCES 2024-25 but not in the 2025-26 NYSED directory. It may have closed or been renamed. Verify before adding it back.
- **One pin per school, not per campus.** The NYC Charter School Center reports about 420 campuses for 285 schools (2025-26), so this map shows fewer locations than exist. The NYSED institution file lists satellite sites by address; adding it would close most of that gap.
- **Count differences.** The NYSED directory has 299 NYC entries and the Charter School Center reports 285 schools. I did not investigate the difference; the two sources may define a "school" differently.
- **Data vintage.** Locations are from the 2024-25 school year. Schools open, close and move.

## Handling discrepancies
When an address on the map does not match what a map search shows, the data is checked in this order, and the first answer found is the source of truth:
1. NYC DOE school page or the school's own website.
2. NYSED and NCES records (the sources used here).
3. Google Maps or other commercial listings, which are often incomplete or list co-located and shared buildings under only one school.

If two official sources agree, the pin stays and the case is noted below. If sources conflict, or only one exists, the school stays on the map but is flagged here until verified. Administrative or network offices are not schools and are intentionally not mapped.

Known cases:
- **604 E 139th St, Bronx 10454** (Success Academy Charter School-Bronx 5 Lower and Upper). NCES lists both at this address, and the NYC DOE school page for Bronx 5 Upper gives the same address and says it shares a building with other schools. Kept. It may not appear as a school on Google Maps.
- **95 Pine St, Manhattan.** Not in either source file, so it is not mapped. It is likely an administrative office rather than a school, but this has not been confirmed. Open item.

## Verification done
- All coordinates fall within New York City's bounding box.
- Every school on the map matched a NYSED directory entry.
- Borough comes from the NCES county field.
- Manual spot-check of pins against real addresses: _to be completed by the author (suggested: 10 random pins)_.

## Refreshing the data
Download the latest NYSED charter directory and NCES public school locations files, and re-run the matching steps above. New schools without an NCES location need an address geocoded.

## Files
- `index.html`: the map (self-contained; Leaflet is embedded; map tiles load from OpenStreetMap).
- `data/charter_schools.csv` and `data/charter_schools.geojson`: the cleaned dataset behind the map.

## How it was built
Built with Claude (Anthropic) for data inspection, matching and page generation, with the sources, matching rules and gaps above reviewed by the author. The NYSED and NCES files are public government data.

Map tiles: © OpenStreetMap contributors. Mapping library: Leaflet (BSD-2-Clause).
