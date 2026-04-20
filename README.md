# SAMHSA ValueSet Viewer

A web application for exploring and analyzing FHIR ValueSets from SAMHSA using tx.fhir.org.

This project now runs behind a Dockerized reverse proxy. Browser requests go to a same-origin `/fhir/` endpoint, and the container proxies those requests to tx.fhir.org server-to-server to avoid browser CORS restrictions.

![SAMHSA ValueSet Viewer](screenshot.png)

## Features

- 🔍 **Browse SAMHSA ValueSets** - Select from a comprehensive list of SAMHSA C2S ValueSets
- 📊 **Detailed Table View** - Display codes with system, version, code, display name, and active status
- ⬆️⬇️ **Sorting** - Click any column header to sort the data
- 🔎 **Filtering** - Filter codes by system, code, or display text in real-time
- 📈 **Statistics** - View summary statistics including total codes, active/inactive counts, and code systems
- 📥 **Export** - Download data in CSV or JSON format
- 📱 **Responsive Design** - Works on desktop and mobile devices
- 🐳 **Docker-Ready** - Nginx container serves the UI and proxies `/fhir/*` to tx.fhir.org

## Quick Start

### Run with Docker Compose

1. Clone this repository:

```bash
git clone https://github.com/SHIFT-Task-Force/samhsa-valueset-viewer.git
cd samhsa-valueset-viewer
```

1. Build and start the container:

```bash
docker compose up --build
```

1. Open your browser to:

```text
http://localhost:8080
```

### Run with Docker (without Compose)

```bash
docker build -t samhsa-valueset-viewer .
docker run --rm -p 8080:80 --name samhsa-valueset-viewer samhsa-valueset-viewer
```

Then open `http://localhost:8080`.

### Why Not GitHub Pages?

GitHub Pages serves static assets only and cannot provide the reverse proxy required for `/fhir/*` requests. Since tx.fhir.org no longer allows browser cross-origin reads for this app's origin, the containerized proxy is required.

## Deployment

### Docker Host / VM Deployment

1. Copy this repository to your host.
2. Run `docker compose up -d --build`.
3. Publish port `8080` directly, or place a TLS reverse proxy in front of it.

### Example: Reverse Proxy at the Edge

If you already have Nginx/Traefik/Caddy at your edge, route traffic for your domain to this container on port `8080`.

### Health Check

The container includes a Docker `HEALTHCHECK` against `/` so orchestrators can detect unhealthy instances.

## Usage

1. **Select a ValueSet** - Choose a SAMHSA ValueSet from the dropdown menu
2. **Fetch Data** - Click the "🔍 Fetch ValueSet" button to retrieve the data
3. **View Results** - The table displays all codes in the ValueSet
4. **Sort** - Click on any column header to sort by that column (click again to reverse)
5. **Filter** - Use the filter inputs to narrow down the displayed codes
6. **Export** - Click "📥 Export to CSV" or "📥 Export to JSON" to download the data

## ValueSets Included

The application includes all SAMHSA C2S (Consent2Share) ValueSets covering:

### Mental Health

- **Mental Health Disorders** (ICD10CM, ICD9CM, LOINC, RXNORM, SNOMED-CT)

### Substance Use Disorders

- **Alcohol Use Disorders** (SNOMEDCD, ICD9CM, RXNORM, ICD10CM, LOINC)
- **Amphetamine Use Disorders** (HCPCS, ICD10CM, ICD9CM, LOINC, RXNORM, SNOMED-CT)
- **Cannabis Use Disorders** (ICD9CM, ICD10CM, LOINC, SNOMED-CT)
- **Cocaine Use Disorders** (ICD10CM, ICD9CM, SNOMED-CT)
- **Hallucinogens** (ICD10CM, ICD9CM, LOINC, SNOMED-CT)
- **Inhalants** (ICD10CM, ICD9CM, SNOMED-CT)
- **Opioids** (ICD10CM, ICD9CM, LOINC, RXNORM, SNOMED-CT, CPT)
- **Other Psychoactive Substances** (SNOMED-CT, ICD9CM, ICD10CM)
- **Sedative/Hypnotic/Anxiolytic Disorders** (SNOMED-CT, ICD10CM, ICD9CM)
- **General Substance Use Information** (HCPCS, LOINC, RXNORM)

### HIV/AIDS

- **HIV/AIDS Information** (HCPCS, ICD9CM, LOINC, RXNORM, SNOMED-CT, CPT)

### Sexual Health

- **Sexuality and Reproductive Health** (ICD9CM, RXNORM)

### Test ValueSets

- **Test Alcohol Use Disorders** (SNOMED-CT)
- **Test HIV/AIDS Information** (SNOMEDCD)

## Technical Details

- **Framework**: Vanilla JavaScript frontend served by Nginx
- **Styling**: Pure CSS with modern features
- **Runtime**: Docker container
- **Proxy**: Nginx reverse proxy (`/fhir/*` -> `https://tx.fhir.org/*`)
- **API**: tx.fhir.org FHIR R4 Terminology Service (via same-origin proxy)
- **Data Format**: FHIR ValueSet resources with expansions
- **Browser Support**: All modern browsers (Chrome, Firefox, Safari, Edge)

## API Information

This application uses a local proxy endpoint that forwards to tx.fhir.org:

**Application Endpoint Pattern:**

```text
/fhir/r4/ValueSet/$expand?url=http%3A%2F%2Fcts.nlm.nih.gov%2Ffhir%2FValueSet%2F{OID}&_format=json
```

**Example:**

```text
/fhir/r4/ValueSet/$expand?url=http%3A%2F%2Fcts.nlm.nih.gov%2Ffhir%2FValueSet%2F2.16.840.1.113762.1.4.1142.36&_format=json
```

The container then proxies this to:

```text
https://tx.fhir.org/r4/ValueSet/$expand?url=http%3A%2F%2Fcts.nlm.nih.gov%2Ffhir%2FValueSet%2F2.16.840.1.113762.1.4.1142.36&_format=json
```

## Related Projects

- **[SLS-ValueSets](https://github.com/SHIFT-Task-Force/SLS-ValueSets)** - The FHIR IG defining these ValueSets
- **[SHIFT Task Force](https://build.fhir.org/ig/SHIFT-Task-Force/slsValueSets/)** - Implementation Guide

## About SAMHSA C2S

The Substance Abuse and Mental Health Services Administration (SAMHSA) Consent2Share (C2S) ValueSets are used to identify sensitive healthcare information related to:

- Mental health and psychiatric care
- Substance use disorders
- HIV/AIDS
- Sexual and reproductive health

These ValueSets support privacy-sensitive consent management in healthcare systems.

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## License

This project is licensed under the same license as the [SLS-ValueSets](https://github.com/SHIFT-Task-Force/SLS-ValueSets) project.

## Support

For issues, questions, or suggestions:

- 🐛 [Open an issue](https://github.com/SHIFT-Task-Force/samhsa-valueset-viewer/issues)
- 💬 [Start a discussion](https://github.com/SHIFT-Task-Force/samhsa-valueset-viewer/discussions)

## Acknowledgments

- Built for the [SHIFT Task Force](https://github.com/SHIFT-Task-Force)
- Uses the [tx.fhir.org](http://tx.fhir.org) terminology service
- SAMHSA ValueSets from the National Library of Medicine's [VSAC](https://vsac.nlm.nih.gov/)
