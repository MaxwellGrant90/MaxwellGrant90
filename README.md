<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner_dark.png">
  <img alt="Velabyte: business intelligence for NYC buildings" src="assets/banner_light.png" width="100%">
</picture>

### Hi, I'm Maxwell Grant, founder of [Velabyte](https://velabyte.app)

I spent eight years on NYC high-rise exterior restoration and construction, on scaffolds and swing stages along the city's facades. Then I learned to build the data side of the industry I came from. **Velabyte** is the result: business intelligence for real estate firms, engineers, architects and construction trades, with ready-made analytics and process automation built on NYC's public building records.

<p>
  <a href="https://velabyte.app"><img alt="velabyte.app" src="https://img.shields.io/badge/velabyte.app-0b1220?style=flat-square&logo=googlechrome&logoColor=00aaff"></a>
  <a href="https://www.linkedin.com/in/maxwell-grant/"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-maxwell--grant-0b1220?style=flat-square&logo=linkedin&logoColor=00aaff"></a>
  <a href="mailto:grantm@velabyte.app"><img alt="Email" src="https://img.shields.io/badge/grantm@velabyte.app-0b1220?style=flat-square&logo=maildotru&logoColor=ffa500"></a>
</p>

---

## Velabyte

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/manhattan_dark.webp">
  <img alt="Live render of Manhattan building footprints with the Flatiron Building lifted out as a facade takeoff" src="assets/manhattan_light.webp" width="100%">
</picture>

<sub>The velabyte.app homepage is a live WebGPU render of real Manhattan footprints from the NYC 3D Building Model. Its scripted tour traces the Ladies' Mile Historic District and lifts the Flatiron Building's facades into a measured takeoff. (Recorded loop, 2× speed.)</sub>

### What it does

<table>
  <tr>
    <td width="33%" valign="top">
      <picture><source media="(prefers-color-scheme: dark)" srcset="assets/building_profile_dark.webp"><img alt="Building Profile" src="assets/building_profile_light.webp" width="100%"></picture>
      <b>Building Profile</b><br><sub>One view of any NYC building: permits and filings, property value and sales, housing and landmark records, and compliance history.</sub>
    </td>
    <td width="33%" valign="top">
      <picture><source media="(prefers-color-scheme: dark)" srcset="assets/facade_compliance_dark.webp"><img alt="Facade Compliance" src="assets/facade_compliance_light.webp" width="100%"></picture>
      <b>Facade Compliance</b><br><sub>Facade Inspection Safety Program (FISP) technical reports with building details, trends and geographic analysis.</sub>
    </td>
    <td width="33%" valign="top">
      <picture><source media="(prefers-color-scheme: dark)" srcset="assets/permit_issuance_dark.webp"><img alt="Permit Issuance" src="assets/permit_issuance_light.webp" width="100%"></picture>
      <b>Permit Issuance</b><br><sub>Permits issued to general contractors, master plumbers, fire suppression, oil burner and sign hanger companies, with trend and geographic analysis.</sub>
    </td>
  </tr>
  <tr>
    <td valign="top">
      <picture><source media="(prefers-color-scheme: dark)" srcset="assets/building_energy_dark.webp"><img alt="Building Energy" src="assets/building_energy_light.webp" width="100%"></picture>
      <b>Building Energy Efficiency</b><br><sub>Exploratory and geographic analysis for sustainability compliance under Local Law 95.</sub>
    </td>
    <td valign="top">
      <picture><source media="(prefers-color-scheme: dark)" srcset="assets/vela_analyst_dark.webp"><img alt="Vela Analyst" src="assets/vela_analyst_light.webp" width="100%"></picture>
      <b>Vela Analyst</b><br><sub>An AI assistant that analyzes every dataset from one workspace, for cross-dataset questions and market insight. In beta.</sub>
    </td>
    <td valign="top">
      <picture><source media="(prefers-color-scheme: dark)" srcset="assets/job_application_dark.webp"><img alt="Job Application" src="assets/job_application_light.webp" width="100%"></picture>
      <b>Job Application</b><br><sub>Engineering and architecture job filings with job details, trends and geographic analysis.</sub>
    </td>
  </tr>
</table>

### How it's built

```mermaid
flowchart LR
  subgraph Sources
    A[NYC Open Data<br/>permits · filings · property · housing · landmarks]
    B[City geometry<br/>3D building model · tax map · districts · open map data]
  end
  L[(Raw lake<br/>source files, as published)]
  subgraph Warehouse["Warehouse · Google BigQuery"]
    C[Bronze<br/>relational model] --> D[Silver<br/>summarized wide tables] --> E[Gold<br/>analysis-ready marts]
  end
  S[Spice AI<br/>accelerated SQL · NL-to-SQL]
  subgraph Serving
    F[Dashboards & reports]
    G[Geospatial snapshots<br/>GeoParquet · SedonaDB]
    H[AI analyst]
  end
  A --> L
  B --> L
  L --> C
  E --> S
  E --> G
  S --> F
  S --> H
```

**Data architecture**
- **Raw lake:** source files land untouched, exactly as the city publishes them, so every load can be replayed and audited.
- **Bronze, relational model:** the raw data is modeled into typed fact and dimension tables with keys and relationships, the system of record for everything above it.
- **Silver, summarized wide tables:** bronze is joined and rolled up into wide, denormalized tables per subject and time grain, so heavy joins happen once in the pipeline, not at query time.
- **Gold, analysis-ready marts:** silver is shaped into marts that each serve a dashboard, map or report directly.
- **Building-centric model:** permits, filings, inspections, sales, assessments, housing and landmark records share one building key from bronze up, so any building's full history is a single lookup and portfolio questions stay a single query.
- **Geometry as first-class data:** 3D building geometry, tax lots and historic district boundaries sit in the warehouse beside the records, so measurements and spatial joins run where the data lives.
- **Containerized pipelines:** ingestion and transforms run as dependency-ordered container jobs on Cloud Run, so each layer rebuilds only after the layers it depends on.
- **Spice AI serving layer:** the Spice AI runtime materializes gold marts into local accelerated copies next to the app, so dashboards query them with low-latency SQL instead of going back to the warehouse. BigQuery stays the source of truth, and map views run spatial queries with SedonaDB over compact GeoParquet snapshots exported from the warehouse, so the app never scans raw data.
- **AI analyst on Spice AI:** plain-English questions become SQL through Spice AI's natural-language-to-SQL, checked and corrected by tools before they run against the same accelerated marts the dashboards use.
- **Documented for people and AI:** every table and column carries a business description and data type, which grounds the analyst's SQL in the real schema.
- **Privacy by design:** public surfaces show signals and tiers computed inside the warehouse, never personal contact details.

**Application**
- **Full-stack Rust:** one codebase compiles to a WebAssembly front end and its server.
- **Encrypted end to end:** application-layer encryption with rotating keys protects every request and response, on top of TLS.
- **Live 3D city on any device:** the skyline renders on the GPU in the browser, and each device gets a short performance probe that falls back to a pre-rendered loop when it can't keep up.
- **Production SaaS:** serverless containers on Google Cloud, transactional and analytical stores kept separate, and subscription billing.

<p>
  <img alt="Rust" src="https://img.shields.io/badge/Rust-0b1220?style=flat-square&logo=rust&logoColor=ffa500">
  <img alt="WebAssembly" src="https://img.shields.io/badge/WebAssembly-0b1220?style=flat-square&logo=webassembly&logoColor=00aaff">
  <img alt="Dioxus" src="https://img.shields.io/badge/Dioxus-0b1220?style=flat-square&logoColor=00aaff">
  <img alt="WebGPU" src="https://img.shields.io/badge/WebGPU%20%C2%B7%20vello-0b1220?style=flat-square&logo=webgpu&logoColor=00aaff">
  <img alt="BigQuery" src="https://img.shields.io/badge/BigQuery-0b1220?style=flat-square&logo=googlebigquery&logoColor=00aaff">
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-0b1220?style=flat-square&logo=postgresql&logoColor=00aaff">
  <img alt="SQLite" src="https://img.shields.io/badge/Turso%20%C2%B7%20SQLite-0b1220?style=flat-square&logo=sqlite&logoColor=00aaff">
  <img alt="Cloud Run" src="https://img.shields.io/badge/Cloud%20Run-0b1220?style=flat-square&logo=googlecloud&logoColor=ffa500">
  <img alt="Spice AI" src="https://img.shields.io/badge/Spice%20AI-0b1220?style=flat-square&logoColor=00aaff">
  <img alt="DuckDB" src="https://img.shields.io/badge/DuckDB-0b1220?style=flat-square&logo=duckdb&logoColor=ffa500">
  <img alt="GeoParquet and SedonaDB" src="https://img.shields.io/badge/GeoParquet%20%C2%B7%20SedonaDB-0b1220?style=flat-square&logo=apacheparquet&logoColor=00aaff">
  <img alt="Stripe" src="https://img.shields.io/badge/Stripe-0b1220?style=flat-square&logo=stripe&logoColor=ffa500">
  <img alt="Python" src="https://img.shields.io/badge/Python-0b1220?style=flat-square&logo=python&logoColor=ffa500">
</p>

<sub>Velabyte's source is private. This page shows the product and how it's built.</sub>

---

## Where it started

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/career_dark.png">
  <img alt="Line chart of NYC DOB jobs per year, 1998 to 2025, for Skyline Restoration, Accura Restoration, Accura Restoration and Waterproofing, and POFI Construction" src="assets/career_light.png" width="100%">
</picture>

The four restoration contractors I worked for during my eight years on NYC facades, measured by DOB jobs per year under each firm's General Contractor license. The data comes from my own BigQuery warehouse (NYC Open Data → raw lake → bronze → silver), queried and drawn in Python with Matplotlib. It's the same warehouse Velabyte runs on.

---

<details>
<summary><b>Earlier work</b>: Tableau, exploratory data analysis, database design</summary>

<br>

**World Happiness Report: Tableau dashboard** ([open the dashboard](https://public.tableau.com/app/profile/maxwell.grant/viz/WorldHappinessReportDashboard_16211719322600/Dashboard1)). I added regions, longitude and latitude to the dataset.

![World Happiness Dashboard](https://user-images.githubusercontent.com/88124878/127759660-bc014a4f-9cd0-4e93-aea0-32e6aa0dfd38.png)

**Exploratory data analysis, linear regression and feature importance** in a Jupyter notebook, with evaluation metrics.

![World Happiness EDA](https://user-images.githubusercontent.com/88124878/127779616-f9edf24b-5c56-4967-a8b1-42b3989d4820.png)
![World Happiness regplot](https://user-images.githubusercontent.com/88124878/127758741-538e366b-5181-49a3-801e-c9ba63733711.png)
![World Happiness correlation](https://user-images.githubusercontent.com/88124878/127779610-2bede530-e348-448b-9184-a4e8ea0067dc.png)
![World Happiness feature importance](https://user-images.githubusercontent.com/88124878/127758744-1d8b7371-5d91-4966-81ec-497f5d5c7962.png)

**Human resources database schema** in third normal form (academic project).

![Entity-Relationship Model](https://user-images.githubusercontent.com/88124878/127951189-8b6599ac-1d8f-4516-aa79-6d3f53a3c659.png)

</details>
