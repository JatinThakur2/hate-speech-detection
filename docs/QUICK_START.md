# ⚡ Quick Start: Run the Notebook Now

## TL;DR - Two Options

### 🚀 Option A: Full Mistral (Best Results, ~2-3 hours)

```bash
# Terminal 1: Install model
ollama pull mistral:latest

# Terminal 1: Start server
OLLAMA_HOST=127.0.0.1:11434 ollama serve

# Terminal 2: VS Code
# Open: advanced_multimodel_hate_speech.ipynb
# Run all cells (top to bottom)
# Shift+Enter on each cell
```

**Result**: Full ensemble with Mistral LLM predictions

---

### ⚡ Option B: Fast Test Without Ollama (~30-60 min)

```bash
# VS Code - Just run it!
# Open: advanced_multimodel_hate_speech.ipynb
# Run all cells (top to bottom)
# Shift+Enter on each cell
```

**Result**: Fast execution with random LLM placeholder (good for testing)

---

## What Happens When You Run

**Cell 1**: ✅ Title & objectives (instant)

**Cells 2-5**: ✅ Load data, setup models (1-2 min)

**Cell 6**:

- Checks for Ollama
- If running: Uses Mistral ✅
- If not: Uses fallback 💡
- Takes ~30 seconds

**Cells 7-8**: Setup training (instant)

**Cell 9**: 🔄 **THE MAIN TRAINING** (1.5-3 hours)

- Trains 3 models on 5 folds
- Shows progress
- Creates ensemble
- Watch the progress output!

**Cells 10-14**: Generate results, visualizations, reports (10-30 min)

---

## Live Progress Indicators

Watch for these in Cell 9 output:

```
EXECUTING 5-FOLD CROSS-VALIDATION
==============================================================================
FOLD 1/5
======================================================================
Training EfficientNet+BERT...
Training CLIP+Text...
Running LLM Zero-Shot (Mistral)...
  Progress: 1/10 batches
  Progress: 2/10 batches
  Fallback rate: 5.0% (1/20)  ← Good! Mistral is working
```

---

## Mistral Status Indicators

| Output                         | Meaning           | Action                     |
| ------------------------------ | ----------------- | -------------------------- |
| `✓ Ollama server is running`   | ✅ Mistral ready  | Run the notebook           |
| `⚠ Ollama server not detected` | 💡 Using fallback | Still works! Faster!       |
| `Fallback rate: 5.0%`          | ✅ Excellent      | Mistral working great      |
| `Fallback rate: 50%+`          | ⚠ Timeouts        | Restart Ollama or skip LLM |

---

## Expected Final Results

### Outputs in notebook folder:

```
📊 CSV Results:
  - cv_results_detailed.csv (all metrics per fold)
  - cv_results_summary.csv (aggregated stats)

📈 Visualizations:
  - model_comparison_detailed.png
  - f1_progression.png
  - confusion_matrices_all.png
  - ensemble_improvement.png
  - roc_curves_all_models.png

📄 Reports:
  - final_report.txt (full analysis)
  - results.json (structured data)
```

---

## If Something Goes Wrong

### "Ollama not found" error

→ Not running. Either install it or continue without it (slower but works)

### "Timeout" in LLM cell

→ Mistral is responding slowly. Fallback activates automatically.

### "500 error" in logs

→ Same as before - restart: `killall ollama` then start fresh

### Cell execution stops

→ Check error message. Usually missing package. Try running cell again.

---

## Performance Expectations

| Setup              | Time      | Mistral Quality       |
| ------------------ | --------- | --------------------- |
| **With Mistral**   | 2-3 hrs   | ✅ Excellent          |
| **Without Ollama** | 30-60 min | 💡 Placeholder (test) |

---

## Commands Reference

```bash
# Install Mistral
ollama pull mistral:latest

# Start server (use this terminal only for serving)
OLLAMA_HOST=127.0.0.1:11434 ollama serve

# Check if running (from another terminal)
curl http://localhost:11434/api/tags

# See available models
ollama list

# Stop server
# Press Ctrl+C in terminal where it's running

# Restart fresh
killall ollama
OLLAMA_HOST=127.0.0.1:11434 ollama serve
```

---

## Need Help?

1. **Setup issues**: Read `MISTRAL_SETUP.md`
2. **Notebook errors**: Check cell output for error message
3. **Too slow**: Using fallback is fine - just testing is faster
4. **Want different model**: See alternative models in `MISTRAL_SETUP.md`

---

## Ready? Let's Go! 🚀

1. Choose Option A or B above
2. Run the notebook
3. Wait for results
4. Check the generated CSV, PNG, and TXT files
5. Done!
