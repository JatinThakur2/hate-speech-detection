# Mistral LLM Setup Guide

## Why Mistral Instead of DeepSeek-R1?

**Mistral advantages**:

- ✅ **10-20x faster**: Optimized for speed and efficiency
- ✅ **Smaller memory footprint**: Works well with 6-8GB VRAM
- ✅ **Lower latency**: Typically 2-5 seconds per inference vs 25-30s for DeepSeek
- ✅ **Better reliability**: Fewer timeout issues
- ✅ **Still accurate**: Excellent for classification tasks
- ✅ **Production-ready**: Widely deployed and tested

**Performance trade-off**:

- DeepSeek-R1: Slower but potentially more reasoning capability
- Mistral: Fast and reliable, excellent for practical classification

---

## Quick Start

### Step 1: Download Mistral Model

```bash
ollama pull mistral:latest
```

This downloads the ~4.4GB Mistral model (takes 2-5 minutes depending on connection).

### Step 2: Start Ollama Server

```bash
ollama serve
```

Or with explicit host/port:

```bash
OLLAMA_HOST=127.0.0.1:11434 ollama serve
```

### Step 3: Verify Installation

```bash
# Check if model is loaded
ollama list

# Quick test
curl -X POST http://localhost:11434/api/generate \
  -H "Content-Type: application/json" \
  -d '{"model": "mistral:latest", "prompt": "Say hello", "stream": false}'
```

### Step 4: Run Notebook

- Open the notebook in VS Code
- Execute all cells from top to bottom
- Notebook will automatically use Mistral if available, fallback to random predictions if not

---

## Automatic Fallback Behavior

The notebook has **built-in resilience**:

```
✓ Ollama running       → Use Mistral LLM (full predictions)
⚠ Ollama unavailable   → Use random predictions (50% confidence)
⚠ Timeout              → Fallback gracefully
⚠ Connection error     → Continue with ensemble of other models
```

**No manual intervention needed!** The notebook detects availability and adjusts automatically.

---

## Expected Performance

### With Mistral (Ollama running):

- ✅ Per-sample inference: 2-5 seconds
- ✅ Fold 1 complete: ~20-40 minutes (depending on fold size)
- ✅ 5-fold CV total: ~2-3 hours

### With Fallback (Ollama not running):

- ⚠ Per-sample inference: <100ms (random prediction)
- ⚠ Fold 1 complete: ~5-10 minutes
- ⚠ 5-fold CV total: ~30-60 minutes (very fast but lower quality LLM component)

---

## Troubleshooting

### Issue: "Ollama server not detected"

**Solution**: Make sure Ollama is running in background

```bash
# Start it in new terminal
OLLAMA_HOST=127.0.0.1:11434 ollama serve
```

### Issue: "Model not found: mistral:latest"

**Solution**: Pull the model first

```bash
ollama pull mistral:latest
```

### Issue: Slow inference (>30s per request)

**Solution**: Check GPU status

```bash
# Verify GPU is being used
ollama list  # Should show GPU memory allocation
```

If still slow:

- GPU might be out of memory
- Try reducing batch size in notebook
- Or use fallback predictions for faster testing

### Issue: 500 errors in logs

**Solution**: Similar to DeepSeek issue - reduce context or restart

```bash
# Restart with fresh state
killall ollama
OLLAMA_HOST=127.0.0.1:11434 ollama serve
```

---

## Alternative Models

If Mistral has issues, try these fast alternatives:

```bash
# Option 1: Neural Chat (even faster)
ollama pull neural-chat:latest

# Option 2: Orca Mini (smallest)
ollama pull orca-mini:latest

# Option 3: Tinyllama (ultra-fast for testing)
ollama pull tinyllama:latest
```

To switch models, edit the notebook cell:

```python
OLLAMA_MODEL = "neural-chat:latest"  # Change this line
```

---

## GPU Memory Requirements

| Model             | VRAM Needed | Status with RTX 3070 Ti (8GB) |
| ----------------- | ----------- | ----------------------------- |
| Mistral (7B)      | 4-5GB       | ✅ Recommended                |
| Neural Chat (7B)  | 4-5GB       | ✅ Works great                |
| Orca Mini (3B)    | 2-3GB       | ✅ Very fast                  |
| TinyLlama (1B)    | 1-2GB       | ✅ Ultra-fast                 |
| DeepSeek-R1 (32B) | 16-20GB     | ❌ Too large                  |

---

## Monitoring During Execution

Watch the notebook output for fallback indicators:

```
Progress: 1/10 batches
Progress: 2/10 batches
  Fallback rate: 15.0% (15/100)  ← Some LLM calls timed out
```

High fallback rates (>50%) indicate:

- Ollama is running but slow
- Consider restarting Ollama or switching to faster model

---

## Questions?

- **Ollama docs**: https://ollama.ai
- **Mistral docs**: https://docs.mistral.ai
- **Model comparison**: Check Ollama model library at ollama.ai/library
