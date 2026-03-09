# ArcGIS Tasks Automation

Automate task archiving, worker offboarding, and contractor registration workflows using the ArcGIS API for Python and Jupyter notebooks.

You will need four ArcGIS Feature Layers for this to work: 

1. Registration Layer - Survey123 Form
2. Source Layer - Tasks Feature Layer
3. Archive Layer - Tasks Feature Layer (same schema as source)
4. Credentials Layer - Contractor credentials with a "delete_today" field 

## Quick Start

### 1. Prerequisites

- **Python 3.10+** (managed by `uv`)
- **uv** package manager: [Install uv](https://docs.astral.sh/uv/getting-started/installation/)
- **ArcGIS Online account** or Enterprise portal access

### 2. Set Up Your Local Environment

Clone or download this project, then initialize it:

```bash
# Navigate to the project directory
cd field-apps-integration-and-automation

# Install dependencies and create the virtual environment
uv sync
```

`uv sync` will:
- Read `pyproject.toml` to identify all dependencies
- Create a `.venv` virtual environment in the project
- Install exact versions from `uv.lock` (ensuring reproducibility)

### 3. Activate the Environment

If you prefer to work with an active shell environment:

```bash
# macOS / Linux
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```

Once activated, you can run Python and Jupyter directly without `uv run`.

### 4. Run the Notebooks

With `uv run` in your terminal

```bash
# Run Contractor Registration workflow
uv run jupyter notebook "Contractor Registration WF.ipynb"

# Run Task Cleanup workflow
uv run jupyter notebook "Tasks Clean Up.ipynb"
```

---

## Project Structure

```
dev-summit/
├── .venv                          # Virtual environment (auto-created)
├── .python-version                # Python version (3.10+)
├── .gitignore                     # Git ignore rules
├── uv.lock                        # Locked dependency versions
├── pyproject.toml                 # Project metadata & dependencies
├── README.md                      # This file
├── Contractor Registration WF.ipynb   # Onboarding automation
└── Tasks Clean Up.ipynb               # Archiving & offboarding
```

### Key Files

- **`pyproject.toml`** — Defines project dependencies:
  - `arcgis>=2.3.0` — ArcGIS API for Python
  - `pandas>=2.0.0` — Data manipulation
  - `notebook>=7.0.0` — Jupyter notebook support
  - `ipykernel>=6.0.0` — Jupyter kernel

- **`uv.lock`** — Reproducible lockfile (check into version control)

- **`.python-version`** — Specifies Python version for the project

---

## ArcGIS Online Authentication

The notebooks support multiple authentication methods. Choose the one that suits your setup.

### 1. **Home Profile (Recommended for Local Development)**

If you are running in the Hosted ArcGIS Online/Enterprise Environment, use:

```python
from arcgis.gis import GIS

gis = GIS("home")
print(f"Logged in as: {gis.properties.user.username}")
```

---

### 2. **Built-In User Account**

For ArcGIS Online or Enterprise with built-in identity:

```python
gis = GIS('https://www.arcgis.com', 'username', 'password')
```

Or for ArcGIS Enterprise:

```python
gis = GIS('https://portalname.domain.com/webadapter', 'username', 'password')
```

---

### 3. **ArcGIS Pro Integration**

If ArcGIS Pro is installed and you're logged in:

```python
gis = GIS("pro")
print(f"Using active portal from ArcGIS Pro: {gis.properties.portalHostname}")
```

---


## Notebook Workflows

### **Contractor Registration.ipynb**

Automates contractor onboarding:
1. Reads new contractor registrations from Survey123
2. Checks for duplicate accounts in ArcGIS Online
3. Creates a new Data Editor / Mobile Worker account
4. Saves credentials to a hosted table
5. Adds the user to a configured group
6. Automatically assigns unassigned tasks at their site

**To use:**
1. Configure the `CONFIG` cell with your layer URLs and field names
2. Run cells top to bottom or run as an hourly script
3. Monitor logs for success/failure messages

---

### **Tasks Clean Up.ipynb**

Automates worker offboarding:
1. Queries credentials layer for workers flagged with `delete_today = YES`
2. Archives their completed tasks to a backup layer
3. Copies all attachments (images, PDFs) to archive records
4. Deletes originals from the active task layer
5. Removes the worker's ArcGIS Online account

**To use:**
1. Flag workers in your credentials layer: set `delete_today = YES`
2. Configure layer URLs in the `CONFIG` cell
3. Run cells top to bottom or run as an hourly script
4. Review the final summary

---

## Additional Resources

- [ArcGIS Python API Documentation](https://developers.arcgis.com/python/latest/)
- [Authentication Schemes Guide](https://developers.arcgis.com/python/latest/guide/working-with-different-authentication-schemes/)
- [uv Documentation](https://docs.astral.sh/uv/)
- [uv Project Guide](https://docs.astral.sh/uv/guides/projects/)

---

## License

See your organization's licensing terms for ArcGIS Online and the ArcGIS Python API.
