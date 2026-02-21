# /map-trip

Generate a KML map file for a trip that can be imported into Google My Maps.

## Usage

```
/map-trip <trip-name>
```

**Parameters:**
- `trip-name` (required): The existing trip folder name (e.g., `osaka-2026`)

## Instructions

1. Parse `$ARGUMENTS` to extract `trip-name`
2. Verify `trips/<trip-name>/overview.md` exists — if not, tell the user to run `/plan-trip` first
3. Use Glob to check that at least one day file exists in `trips/<trip-name>/itinerary/` — if not, tell the user to run `/build-itinerary` first
4. Delegate to the **kml-generator** agent:
   - Pass the trip name
   - The agent reads each day file, extracts locations, finds coordinates via WebSearch, and writes the KML
5. When the agent completes, confirm the output path and print import instructions:
   1. Go to [maps.google.com/maps/d](https://maps.google.com/maps/d) → Create a new map
   2. Click **Import** → upload `trips/<trip-name>/<trip-name>.kml`
   3. Each day appears as its own toggle-able layer

## Agent Delegation

agent: kml-generator
context: fork

Pass to the agent:
- Trip name: `<trip-name>`
- Trip folder: `trips/<trip-name>/`
