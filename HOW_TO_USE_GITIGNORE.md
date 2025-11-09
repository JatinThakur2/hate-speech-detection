# 🚀 How to Use .gitignore with Your Project

## Step 1: Verify .gitignore Is Working

```bash
cd "c:\Users\NZXT\Desktop\Papers\Hate speech detection"

# Check Git status
git status

# You should see ONLY:
# - .gitignore
# - .ipynb files
# - .md files
# - requirements.txt
# - Any other source files

# You should NOT see:
# - __pycache__/
# - .ipynb_checkpoints/
# - data/ folder
# - *.pth files
# - *.csv files
# - *.png files
```

---

## Step 2: Initial Commit (First Time)

```bash
# 1. Add .gitignore first
git add .gitignore

# 2. Commit it
git commit -m "Add .gitignore for ML project"

# 3. Add all source code (respects .gitignore)
git add .

# 4. Commit
git commit -m "Add ML pipeline code and documentation"

# 5. Push to remote (if using GitHub)
git push origin main
```

---

## Step 3: Day-to-Day Workflow

```bash
# After making code changes
git add .                    # Add changes (ignores large files)
git commit -m "your message"
git push origin main

# View what's being tracked
git ls-files

# View what's being ignored
git status --ignored
```

---

## Common Scenarios

### Scenario 1: I Generated Results, Should I Commit Them?
```bash
# Results like .csv, .png, .json are REGENERABLE
# Better to NOT commit them
# Users can run the notebook themselves

# If you want to show results, consider:
# - Upload to separate releases
# - Add screenshots to README
# - Store in results/ folder (not in Git)

git check-ignore -v cv_results_detailed.csv
# Output: cv_results_detailed.csv  matching pattern *.csv

✅ IGNORED (Good!)
```

### Scenario 2: I Want to Commit a Model File
```bash
# Model files are ignored for good reason (too large)
# But if you REALLY need to:

# Option 1: Use Git LFS
git lfs install
git lfs track "*.pth"
git add best_model.pth

# Option 2: Use cloud storage
# - Upload to HuggingFace Model Hub
# - Upload to Cloud Storage (S3, Google Drive)
# - Add link in README

# Option 3: Use DVC (Data Version Control)
dvc init
dvc add best_model.pth
```

### Scenario 3: I Accidentally Tracked a Large File
```bash
# Remove from Git without deleting locally
git rm --cached large_file.pth
git commit -m "Remove large file from tracking"

# It will be ignored next time because of .gitignore
```

### Scenario 4: I Need to Share Secrets (.env)
```bash
# NEVER commit .env or secrets.json
# Instead:

# 1. Create .env.example
cat > .env.example << EOF
OLLAMA_HOST=localhost:11434
API_KEY=your_key_here
EOF

# 2. Commit .env.example (no real values)
git add .env.example

# 3. .env stays ignored (Git will skip it)
git status  # .env not shown

# 4. Users copy and fill in:
cp .env.example .env
# Then fill in real values locally
```

---

## Repository Management

### Check Repository Size
```bash
# See how big it is
git count-objects -vH

# See largest files
git rev-list --all --objects | sort -k2 -r | head -20
```

### Clean Up Old Files
```bash
# Remove cached ignored files
git rm -r --cached .

# Re-add everything (will respect .gitignore)
git add .

# Commit
git commit -m "Clean up ignored files"
```

### Exclude More Files?
```bash
# Just add to .gitignore and commit
echo "*.tmp" >> .gitignore
git add .gitignore
git commit -m "Ignore .tmp files"
```

---

## For Your Specific Project

### What to Track ✅

```bash
# When pushing to GitHub:
git add advanced_multimodel_hate_speech.ipynb
git add QUICK_START.md
git add MISTRAL_SETUP.md
git add requirements.txt
git add .gitignore
git add GITIGNORE_GUIDE.md

git commit -m "Add ML pipeline with documentation"
git push origin main
```

### What NOT to Track ❌

```bash
# These will be automatically ignored:
# data/
# .ollama/
# *.pth (model files)
# *.csv (results)
# *.png (visualizations)
# __pycache__/
# .vscode/
# .env

# You don't need to do anything - .gitignore handles it!
```

---

## Setup GitHub Repository

### Step 1: Create Repo on GitHub

Go to github.com and create new repository:
- Name: `hate-speech-detection`
- Description: "Advanced multi-model hate speech detection with CLIP, BERT, and Mistral LLM"
- Public or Private (your choice)
- Do NOT initialize with README (you have one)

### Step 2: Connect Local to Remote

```bash
cd "c:\Users\NZXT\Desktop\Papers\Hate speech detection"

# Add remote
git remote add origin https://github.com/YOUR_USERNAME/hate-speech-detection.git

# Rename branch to main (if needed)
git branch -M main

# Push everything
git push -u origin main
```

### Step 3: Verify on GitHub

Check github.com and you should see:
- ✅ .ipynb notebooks
- ✅ .md documentation
- ✅ requirements.txt
- ✅ .gitignore

But NO:
- ❌ data/ folder
- ❌ *.pth files
- ❌ *.csv results
- ❌ *.png visualizations

---

## Common .gitignore Issues

### Issue: File still appears in git status
```bash
# Solution: File was already tracked before .gitignore
git rm --cached filename.pth
git commit -m "Stop tracking large file"
```

### Issue: Can't find something in repository
```bash
# Check if it's ignored
git check-ignore -v missing_file.txt

# If ignored, check .gitignore pattern
cat .gitignore | grep "missing_file"
```

### Issue: Want to track file that matches .gitignore
```bash
# Force add it
git add -f special_model.pth

# But think twice - is it really needed?
```

---

## Final Checklist

Before pushing to GitHub:

```
✅ .gitignore created and committed
✅ Source code (.py, .ipynb) added
✅ Documentation (.md files) added
✅ requirements.txt added
✅ Large files NOT added (*.pth, data/, etc.)
✅ Secrets NOT added (.env, secrets.json)
✅ Repository size reasonable (< 10 MB)
✅ Remote repository configured (git remote -v)
✅ Able to push successfully (git push)
✅ GitHub shows code, not data
```

---

## Quick Reference

```bash
# Show what will be committed
git status

# Commit all changes (respects .gitignore)
git add .
git commit -m "message"

# Push to GitHub
git push origin main

# View all tracked files
git ls-files

# View all ignored files
git status --ignored

# Check if file is ignored
git check-ignore -v filename
```

**Your project is ready for Git!** 🚀
