# Catch

Catch is a mobile website for students who ride FrontRunner to campus. It shows every train and bus connection for your commute in one view, with a countdown to the next one you need to catch.

I built it for my own commute from Holladay to BYU. That trip is a car or bus to Murray Central, FrontRunner to Provo Central, then the UVX bus to campus. Google Maps shows one route at a time, so it was hard to see all my options at once or know how long I'd have to make the transfer. Catch lays them all out together.

## What it does

- **My Trips.** Save a commute you take often, like "Home to BYU," and open it with one tap. Trips are sorted by when you usually take them, so the next one you need is at the top.
- **Up next with a countdown.** Each trip shows the next train, the bus it connects to, and how many minutes you have. The countdown turns amber when it's getting close and red when you're about to miss it.
- **Transfers spelled out.** Every option shows where you switch from the train to the bus, when the bus leaves, and how much time you have to walk over.
- **Arrive by.** Pick a time you need to be on campus and Catch finds the latest train that still gets you there.
- **Plan a one-time trip.** Pick any two stations for a trip you don't take often, and save it to My Trips if you want to keep it.
- **Both directions.** Morning trips to campus and evening trips home, including the next morning's trips once the last train of the night has left.
- **Real schedules.** Times come straight from UTA's public schedule data, so they match what the trains and buses actually run.

## How it works

Catch downloads UTA's public transit schedule (the GTFS feed) and reads the FrontRunner and UVX trips for the day. It matches each train to the buses that leave after it arrives, leaving a few minutes to walk between the platform and the bus bay. The website is built with Python and Flask and is designed to be used on a phone.

| File | What it does |
| --- | --- |
| `app.py` | The website and its pages |
| `frontrunner.py` | Downloads and reads UTA's schedule data |
| `commute.py` | Matches trains to bus connections, both directions |
| `uvx.py` | UVX bus schedule between Provo Central and BYU |
| `planner.py` | Finds trips between any two stations |
| `trips.py` | Saves and loads My Trips |
| `templates/` | The page designs |

## Run it

Requires Python 3.10 or newer.

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/python app.py           # open http://localhost:8080
.venv/bin/python app.py --phone   # also open it on your phone over the same Wi-Fi
```

The first run downloads UTA's schedule, which takes a few seconds. Add `--refresh` to get the latest schedule.

## What's next

- Accounts, so each student has their own saved trips
- Live train delays from UTA
- Money and time saved by riding instead of driving
