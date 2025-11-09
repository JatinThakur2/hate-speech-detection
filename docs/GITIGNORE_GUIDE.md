# .gitignore Explanation

## What's Ignored

### 🐍 Python Files

- `__pycache__/` - Python cache directories
- `*.pyc, *.pyo, *.pyd` - Compiled Python files
- Virtual environments: `env/`, `venv/`, `.venv/`
- Build artifacts: `build/`, `dist/`, `*.egg-info/`

### 📓 Jupyter Notebooks

- `.ipynb_checkpoints/` - Notebook checkpoint files
- These are auto-generated and shouldn't be tracked

### 💻 IDE Files

- `.vscode/` - VS Code settings
- `.idea/` - PyCharm settings
- `*.swp, *.swo` - Vim/Vi temporary files
- `.DS_Store` - macOS folder metadata

### 🤖 ML Models & Data

- `*.pth` - PyTorch models
- `*.pkl` - Pickle files
- `*.h5` - HDF5 model files
- `data/` - Large datasets
- These are large files (often 100MB+) and slow down Git

### 📊 Generated Results

- `*.csv` - Results dataframes
- `results.json` - JSON exports
- `*.png, *.jpg` - Generated visualizations
- `final_report.txt` - Text reports
- **Note**: These can be regenerated from code, so no need to track

### 🦙 Ollama Cache

- `.ollama/` - Local LLM cache
- `ollama_models/` - Downloaded models
- These are downloaded and rebuilt as needed

### 📝 Logs & Temp Files

- `*.log` - Log files
- `*.tmp, *.bak` - Temporary backups
- `.cache/` - Cache directories

### 🔐 Sensitive Files

- `.env` - Environment variables
- `secrets.json` - API keys, credentials
- Never commit these!

---

## What's NOT Ignored (Will Be Tracked)

✅ **Source Code**:

- `*.py` - Python scripts
- `*.ipynb` - Jupyter notebooks themselves (but not checkpoints)
- `*.md` - Documentation

✅ **Configuration**:

- `requirements.txt` - Package dependencies
- `setup.py` - Setup configuration
- `.gitignore` - This file itself

✅ **Documentation**:

- `README.md`
- `QUICK_START.md`
- `MISTRAL_SETUP.md`
- All `*.md` files

---

## Key Points for This Project

### ✅ Should Commit:

```
advanced_multimodel_hate_speech.ipynb  ✓ (the code)
QUICK_START.md                         ✓ (documentation)
MISTRAL_SETUP.md                       ✓ (setup guide)
requirements.txt                       ✓ (dependencies)
```

### ❌ Should NOT Commit:

```
*.pth                                  ✗ (model files, too large)
*.csv                                  ✗ (results, regenerable)
*.png                                  ✗ (visualizations, regenerable)
data/                                  ✗ (large datasets)
.ipynb_checkpoints/                    ✗ (auto-generated)
__pycache__/                           ✗ (auto-generated)
```

---

## Usage

The `.gitignore` file is automatically used by Git. Just commit it once:

```bash
git add .gitignore
git commit -m "Add .gitignore for Python ML project"
```

Then Git will automatically ignore all listed files/folders.

---

## Common Commands

```bash
# See what will be tracked
git status

# Track specific file despite .gitignore
git add -f filename.txt

# Remove file from Git but keep locally
git rm --cached filename.txt

# Check if file is ignored
git check-ignore filename.txt
```

---

## Size Comparison

With proper `.gitignore`:

- ✅ Repository size: ~1-5MB (just code)
- ❌ Without .gitignore: Could be 500MB-1GB+ (models + data)

**Result**: Faster cloning, pushing, and collaborating! 🚀
