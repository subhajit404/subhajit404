# 👋 Subhajit Patra


## ⚠️ Disclaimer

<img align="left" width="60" src="https://user-images.githubusercontent.com/74038190/216122041-518ac897-8d92-4c6b-9b3f-ca01dcaf38ee.png">

### Building real ML systems — not just studying them.

---

## 🎓 Quick Snapshot

- 🧠 4th-year **AI & ML** undergraduate  
- 🛠️ Hands-on experience: classification/regression models, data pipelines & deployment  
- 💼 **AI Intern** @ **CodeClause**  

---

## 💻 Tech Stack

<img align="left" width="60" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" style="animation: spin 3s linear infinite;">
<style>
@keyframes spin { 100% { transform: rotate(360deg); } }
</style>

- Python · Pandas · NumPy  
- 🤖 Scikit-learn · TensorFlow / PyTorch  
- 📊 Data Viz: Matplotlib, Seaborn  

---

## 🌟 What Sets Me Apart

- 🚀 Active in **GDG Kolkata** — close to dev trends & community  
- 🎨 Content creation background → I explain complex ML clearly  

---

<div align="center">

**📫 Let's build something that matters.**

</div>

from PIL import Image, ImageOps
from pathlib import Path
import math

src = Path("/mnt/data/ddad6332-af39-4c90-9e37-2e66ebdaf909.png")
out_dir = Path("/mnt/data/animated_logo")
out_dir.mkdir(exist_ok=True)

img = Image.open(src).convert("RGBA")

# Crop the small surrounding margin while preserving the logo.
bbox = img.getbbox()
img = img.crop(bbox)

# Make a simple animated logo GIF: gentle breathing/rotation and a slight horizontal
# "snake-like" motion, while keeping the original artwork intact.
W, H = img.size
canvas_size = max(W, H) + 40
frames = []

for i in range(16):
    t = i / 16 * 2 * math.pi
    angle = 2.2 * math.sin(t)
    scale = 1.0 + 0.025 * math.sin(t)
    dx = 4 * math.sin(t)
    dy = 3 * math.cos(t)

    w = int(W * scale)
    h = int(H * scale)
    frame = img.resize((w, h), Image.Resampling.LANCZOS)
    frame = frame.rotate(angle, resample=Image.Resampling.BICUBIC, expand=True)

    # White canvas to match the original appearance.
    canvas = Image.new("RGBA", (canvas_size, canvas_size), "white")
    x = int((canvas_size - frame.width) / 2 + dx)
    y = int((canvas_size - frame.height) / 2 + dy)
    canvas.alpha_composite(frame, (x, y))
    frames.append(canvas.convert("RGB"))

gif_path = out_dir / "animated_logo.gif"
frames[0].save(
    gif_path,
    save_all=True,
    append_images=frames[1:],
    duration=90,
    loop=0,
    optimize=True,
)

md_path = out_dir / "animated_logo.md"
md_text = """# Animated Logo

![Animated Logo](animated_logo.gif)

> Animated version of the supplied logo with a subtle looping motion.
"""
md_path.write_text(md_text, encoding="utf-8")

print(f"Created:\n- {md_path}\n- {gif_path}")

