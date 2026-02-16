# /research-destination

Research a destination for an existing trip, producing a comprehensive research document.

## Usage

```
/research-destination <trip-name> <destination>
```

**Parameters:**
- `trip-name` (required): The existing trip folder name (e.g., `tokyo-2026`)
- `destination` (required): The destination to research (e.g., `Tokyo`, `Paris`, `Bali`)

## Instructions

1. Parse `$ARGUMENTS` to extract `trip-name` and `destination`
2. Verify that `trips/<trip-name>/overview.md` exists — if not, tell the user to run `/plan-trip` first
3. Read `trips/<trip-name>/overview.md` to get trip dates, budget level, and traveler info
4. Delegate to the **travel-researcher** agent using `context: fork`:
   - Pass the trip name, destination, travel dates, and budget level
   - The agent will use WebSearch and WebFetch to research the destination
   - The agent will write the output to `trips/<trip-name>/research/<destination-kebab>.md`
5. Once complete, confirm the research file was created and suggest next steps:
   - Review the research document
   - `/build-itinerary <trip-name>` to create day-by-day plans
   - `/research-destination <trip-name> <other-destination>` if the trip includes multiple destinations

## Agent Delegation

```
agent: travel-researcher
context: fork
```

Pass to the agent:
- Trip name: `<trip-name>`
- Destination: `<destination>`
- Trip overview path: `trips/<trip-name>/overview.md`
- Output path: `trips/<trip-name>/research/<destination-kebab>.md`
