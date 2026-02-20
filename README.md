# SAMHSA ValueSet Viewer

A web application for exploring and analyzing FHIR ValueSets from SAMHSA using tx.fhir.org.

🔗 **Live Demo**: [https://shift-task-force.github.io/samhsa-valueset-viewer/](https://shift-task-force.github.io/samhsa-valueset-viewer/)

![SAMHSA ValueSet Viewer](screenshot.png)

## Features

- 🔍 **Browse SAMHSA ValueSets** - Select from a comprehensive list of SAMHSA C2S ValueSets
- 📊 **Detailed Table View** - Display codes with system, version, code, display name, and active status
- ⬆️⬇️ **Sorting** - Click any column header to sort the data
- 🔎 **Filtering** - Filter codes by system, code, or display text in real-time
- 📈 **Statistics** - View summary statistics including total codes, active/inactive counts, and code systems
- 📥 **Export** - Download data in CSV or JSON format
- 📱 **Responsive Design** - Works on desktop and mobile devices

## Quick Start

### View Online

Visit [https://shift-task-force.github.io/samhsa-valueset-viewer/](https://shift-task-force.github.io/samhsa-valueset-viewer/) to use the app immediately.

### Run Locally

1. Clone this repository:
```bash
git clone https://github.com/SHIFT-Task-Force/samhsa-valueset-viewer.git
cd samhsa-valueset-viewer
```

2. Open `index.html` in your web browser, or use a local server:

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js http-server
npx http-server -p 8000
```

Then open your browser to `http://localhost:8000`

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

## Deployment to GitHub Pages

### Automatic Deployment (GitHub Settings)

1. Push this repository to GitHub
2. Go to **Settings** > **Pages**
3. Under "Source", select:
   - Branch: `main`
   - Folder: `/ (root)`
4. Click **Save**
5. Your site will be published at `https://[your-username].github.io/samhsa-valueset-viewer/`

### Using GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## Technical Details

- **Framework**: Vanilla JavaScript (no dependencies)
- **Styling**: Pure CSS with modern features
- **API**: tx.fhir.org FHIR R4 Terminology Service
- **Data Format**: FHIR ValueSet resources with expansions
- **Browser Support**: All modern browsers (Chrome, Firefox, Safari, Edge)

## API Information

This application uses the tx.fhir.org FHIR Terminology Service:

**Endpoint Pattern:**
```
https://tx.fhir.org/r4/ValueSet/$expand?url=http%3A%2F%2Fcts.nlm.nih.gov%2Ffhir%2FValueSet%2F{OID}&_format=json
```

**Example:**
```
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
