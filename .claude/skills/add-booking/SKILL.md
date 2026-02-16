# /add-booking

Add a flight, hotel, or activity booking to an existing trip.

## Usage

```
/add-booking <trip-name> <flight|hotel|activity>
```

**Parameters:**
- `trip-name` (required): The existing trip folder name (e.g., `tokyo-2026`)
- `type` (required): One of `flight`, `hotel`, or `activity`

## Instructions

1. Parse `$ARGUMENTS` to extract `trip-name` and booking type
2. Verify that `trips/<trip-name>/overview.md` exists — if not, tell the user to run `/plan-trip` first
3. Read the existing bookings file at `trips/<trip-name>/bookings/<type>s.md`
4. Use `AskUserQuestion` to gather booking details based on type:

### Flight Details
- Airline and flight number
- Route (from → to)
- Date and times (departure → arrival)
- Confirmation/booking reference
- Cost
- Status (booked / pending / waitlisted)

### Hotel Details
- Hotel name
- Check-in and check-out dates
- Room type
- Confirmation/booking reference
- Cost (total or per night)
- Status (booked / pending)

### Activity Details
- Activity name
- Date and time
- Location
- Confirmation/booking reference (if any)
- Cost
- Status (booked / pending / free)

5. Append the new booking as a row in the bookings table in the appropriate file
6. Update the booking count and total cost at the bottom of the file
7. Read `trips/<trip-name>/overview.md` and update the Budget Tracker table with the new booked amount for the relevant category
8. Confirm the booking was added and show the updated totals
