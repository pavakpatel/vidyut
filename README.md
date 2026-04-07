# Vidyut.

**India's Live Energy Infrastructure Tracker**

Vidyut aggregates data from 12 API endpoints published by the [Central Electricity Authority (CEA)](https://cea.nic.in) into a single, interactive dashboard — tracking India's installed capacity, power generation, renewable growth, supply-demand balance, transmission infrastructure, and per-capita consumption across every state and union territory.

**Live site:** [https://pavakpatel.github.io/vidyut](https://pavakpatel.github.io/vidyut)

---

## What's tracked

| Section | Data | Source endpoint |
|---------|------|-----------------|
| Overview | Total installed capacity by fuel type | `installed_capacity_allindia` |
| Capacity | Region-wise & state-wise breakdown | `installed_capacity`, `installed_capacity_statewise` |
| Generation | Monthly generation by mode (BU) | `power_generation` |
| Renewables | Solar, wind, biomass, small hydro growth | `instcap_allindia_res`, `renewable_energy` |
| Supply Position | Energy requirement vs availability | `psp_energy`, `psp_peak` |
| Infrastructure | Transmission lines & substations | `transmission_lines`, `transformation_substations` |
| Per Capita | State-wise kWh consumption | `percapitalConsumtion` |

## How it works

1. **GitHub Actions** runs daily at 6:00 AM IST, fetching all 12 CEA API endpoints
2. JSON responses are committed to the `data/` directory
3. The frontend (`index.html`) reads from `./data/*.json` — pure static files
4. Hosted on **GitHub Pages** — no backend, no proxy, no API keys

```
.github/workflows/fetch-data.yml   ← Scheduled data fetcher
data/*.json                         ← Pre-fetched CEA data (auto-updated)
index.html                          ← Dashboard (single file, no build step)
```

## Run locally

```bash
# Any static file server works
python3 -m http.server 8080
# Open http://localhost:8080
```

## Update data manually

```bash
# Trigger the GitHub Action
gh workflow run fetch-data.yml

# Or fetch locally
curl -sk https://cea.nic.in/api/installed_capacity_allindia.php -o data/installed_capacity_allindia.json
```

## Data source

All data is sourced from the [Central Electricity Authority](https://cea.nic.in/api-for-central-electricity-authority-data/?lang=en), Government of India, Ministry of Power. This project is not affiliated with or endorsed by CEA.

---

Built by [Pavak Patel](https://github.com/pavakpatel)
