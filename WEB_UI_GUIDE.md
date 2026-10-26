# Clinical Decision Support Agent - Web UI

## Quick Start Guide

### 1. Install Flask (if not already installed)
```bash
pip install flask==3.0.0
```

### 2. Start the Web Application
```bash
python app.py
```

### 3. Access the Web Interface
Open your browser and navigate to:
```
http://localhost:5000
```

## Features

### Web Interface
- **Live Patient Data Entry**: Enter patient information through an intuitive web form
- **Real-Time Analysis**: Submit data and get AI-powered clinical decision support
- **Interactive Results**: View differential diagnosis, treatment options, safety alerts, and evidence citations
- **Report Downloads**: Download generated reports in JSON, Markdown, and Citations formats
- **Data Persistence**: Patient data is automatically saved to the database

### Report Management
- **Automatic Cleanup**: System maintains only the last 7 reports automatically
- **Configurable Retention**: Adjust `max_reports` in config.yaml to change retention policy

### API Endpoints

#### POST /api/analyze
Submit patient data for analysis
- **Input**: JSON with patient information
- **Output**: Clinical decision support summary with confidence scores, diagnoses, treatments, and safety alerts

#### GET /api/reports
List all available reports
- **Output**: List of reports with metadata (patient_id, timestamp, confidence score)

#### GET /api/reports/<run_id>
Get specific report by run_id
- **Output**: Full report JSON data

#### GET /reports/<filename>
Download report file (JSON, MD, or citations)

## Form Fields

### Required Fields
- **Age**: Patient age (0-120)
- **Sex**: Male or Female
- **Chief Complaint**: Primary reason for visit

### Optional Fields
- **Patient ID**: Auto-generated if not provided
- **Weight & Height**: For dosing calculations
- **History of Present Illness**: Detailed description
- **Allergies**: Comma-separated list
- **Current Medications**: Comma-separated list
- **Past Medical History**: Comma-separated conditions
- **Vital Signs**: BP, HR, Temperature, RR, SpO2

## Example Usage

### 1. Fill out the patient form on the left
```
Age: 45
Sex: Male
Chief Complaint: Chest pain for 2 hours
History: Substernal chest pain, radiating to left arm
Allergies: Penicillin
Current Medications: Metformin 500mg, Lisinopril 10mg
Past Medical History: Diabetes Type 2, Hypertension
Vital Signs: BP 140/90, HR 95 bpm
```

### 2. Click "Analyze Patient"
The system will:
- Process the patient data
- Query the RAG knowledge base
- Run safety guardrails
- Generate differential diagnosis
- Recommend treatments with evidence
- Identify safety concerns

### 3. View Results
Results appear in real-time:
- **Confidence Score**: Overall analysis confidence
- **Differential Diagnosis**: Top 5 possible diagnoses with probabilities
- **Treatment Options**: Evidence-based medication recommendations
- **Safety Alerts**: Drug interactions, allergies, contraindications
- **Citations**: Evidence sources with levels of evidence

### 4. Download Reports
Click download buttons to get:
- **JSON**: Machine-readable full report
- **Markdown**: Human-readable report
- **Citations**: Evidence sources and references

## Configuration

Edit `config.yaml` to customize:
```yaml
output:
  report_dir: ./reports
  max_reports: 7  # Keep only last 7 reports
  log_path: ./agent.log
  log_level: INFO
```

## Data Storage

Patient data submitted through the web UI is automatically saved to:
```
data/patients.csv
```

This allows:
- Data persistence across sessions
- Historical patient tracking
- Ability to re-run analysis on existing patients

## Safety Features

- **HIPAA Compliance**: Enabled by default
- **GDPR Compliance**: Enabled by default
- **Input Validation**: Sanitizes all user inputs
- **PII Detection**: Monitors for sensitive data
- **Audit Logging**: All actions are logged
- **Safety Guardrails**: Validates all recommendations

## Troubleshooting

### Port Already in Use
If port 5000 is in use, edit app.py:
```python
app.run(debug=True, host='0.0.0.0', port=5001)
```

### Connection Refused
Ensure the LLM backend (Ollama) is running:
```
http://34.207.216.209:11434
```

### Slow Response Times
Analysis typically takes 30-60 seconds depending on:
- LLM response time
- RAG query complexity
- Number of safety checks

### Error Messages
Check the console output and `agent.log` for detailed error information.

## Architecture

```
Browser (User Input)
    ↓
Flask Web Server (app.py)
    ↓
Clinical Decision Agent
    ├── RAG Engine (Evidence Retrieval)
    ├── LLM Client (Ollama/Llama)
    ├── Guardrail Pipeline (Safety Checks)
    └── Reporter (Output Generation)
    ↓
Reports + Data Storage
```

## Next Steps

1. Customize the UI styling in `templates/index.html`
2. Add authentication for production use
3. Implement user session management
4. Add report history browsing
5. Enable report comparison features
6. Add export to EMR systems

## Support

For issues or questions, check:
- `agent.log` for application logs
- `audit_logs/` for audit trails
- `reports/` for generated reports
