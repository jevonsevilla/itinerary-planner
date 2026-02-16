# /plan-trip

Create a new trip folder structure with overview and empty booking files.

## Usage

```
/plan-trip <trip-name> [destination] [dates] [budget-level]
```

**Parameters:**
- `trip-name` (required): Kebab-case name for the trip (e.g., `tokyo-2026`)
- `destination` (optional): Primary destination city/country
- `dates` (optional): Travel dates (e.g., `"2026-04-01 to 2026-04-08"`)
- `budget-level` (optional): One of `budget`, `mid-range`, `luxury` (default: `mid-range`)

If optional parameters are not provided, ask the user interactively.

## Instructions

1. Parse the arguments from `$ARGUMENTS`. The format is: `<trip-name> [destination] [dates] [budget-level]`
2. If destination, dates, or budget-level are missing, use `AskUserQuestion` to gather them
3. Calculate the number of trip days from the date range
4. Create the folder structure under `trips/<trip-name>/`:
   ```
   trips/<trip-name>/
   ├── overview.md
   ├── research/
   ├── itinerary/
   └── bookings/
       ├── flights.md
       ├── hotels.md
       └── activities.md
   ```
5. Generate `overview.md` using the template at `.claude/skills/plan-trip/templates/trip-overview.md`, filling in all variables
6. Generate empty booking files using the template at `.claude/skills/plan-trip/templates/booking.md`
7. Display a summary of what was created and suggest next steps:
   - `/research-destination <trip-name> <destination>` to research the destination
   - `/add-booking <trip-name> flight` to add known bookings
