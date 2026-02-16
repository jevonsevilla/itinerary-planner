# /build-itinerary

Build a day-by-day itinerary for an existing trip based on research and bookings.

## Usage

```
/build-itinerary <trip-name>
```

**Parameters:**
- `trip-name` (required): The existing trip folder name (e.g., `tokyo-2026`)

## Instructions

1. Parse `$ARGUMENTS` to extract `trip-name`
2. Verify that `trips/<trip-name>/overview.md` exists — if not, tell the user to run `/plan-trip` first
3. Check that at least one research document exists in `trips/<trip-name>/research/` — if not, suggest running `/research-destination` first
4. Delegate to the **itinerary-builder** agent using `context: fork`:
   - Pass the trip name
   - The agent will read overview, research docs, and bookings
   - The agent will use WebSearch to look up travel times, opening hours, etc.
   - The agent will create day files at `trips/<trip-name>/itinerary/day-NN.md`
5. Once complete, confirm the itinerary was created and suggest next steps:
   - Review each day's plan
   - `/add-booking <trip-name> activity` to book specific activities
   - `/trip-summary <trip-name>` for a full trip overview

## Agent Delegation

```
agent: itinerary-builder
context: fork
```

Pass to the agent:
- Trip name: `<trip-name>`
- Trip folder: `trips/<trip-name>/`
