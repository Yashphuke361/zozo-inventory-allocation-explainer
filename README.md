# zozo-inventory-allocation-explainer
2.5-min animated explainer of the Gurobi case “ZOZO Research: Optimizing Inventory Allocation for Scalable E-Commerce Logistics”. Built in Python (Skia + AI voiceover). BMN 616, DoMS IIT Roorkee.

📦 The Life of One Order: ZOZO Inventory Allocation, Explained

A 2½-minute animated explainer of the Gurobi case study "ZOZO Research: Optimizing Inventory Allocation for Scalable E-Commerce Logistics", built entirely in code (Python + Skia + an AI voiceover).

Course: BMN 616 – Advanced Optimization Techniques for Managers · Case-based Project Institute: Department of Management Studies, IIT Roorkee

Team member	Roll no.
Aditya Surya	25810005
Yash Phuke	25810066
Chirag Sharma	25810053
▶️ Watch the video

Watch the video

Click here to play ZOZO_Life_of_One_Order.mp4 (2:25 · 1080p · captions burnt in)

The full narration with timestamps is in docs/voiceover-script.md.

🧩 The case in 60 seconds

ZOZO, Inc. runs ZOZOTOWN, Japan's large fashion e-commerce platform, and its own logistics centres, ZOZOBASE. These handle everything in-house: receiving, inspection, photography, storage, picking, packing and shipping.

The problem. When two new logistics centres opened, storage capacity across the Narashino and Tsukuba areas changed significantly. Most ZOZOTOWN orders ship as a single package, so if items bought together sit in different centres, one has to be transferred before shipping. Each transfer adds cost, time and operational complexity. Letting inventory or workload pile up in one centre was a second, long-term risk.

The idea. Instead of modelling millions of individual orders, ZOZO Research aggregated historical orders at the shop level. Shops that are frequently bought together are allocated to the same centre wherever possible.

The optimization model (mixed-integer program).

Element	In this case
Decision	Which logistics centre each shop's inventory is allocated to
Objective	Minimise the number of orders that need fulfilment from more than one centre
Capacity constraints	Per facility: inventory volume and operational throughput (receiving, inspection, shipping)
Balance constraints	Prevent imbalances in inventory distribution and utilisation rates across facilities

The solver story. With open-source solvers, even the LP relaxations of the MILP took far longer than expected. Gurobi's support for multiple LP algorithms (barrier and simplex) let the team test approaches and get substantial speed-ups. Along the way they found the bottleneck was structural, in the problem itself, not the solver.

Results.

Minimised inter-facility transfers through data-driven inventory allocation.
2020: the model guided allocation between Narashino and Tsukuba for the opening of ZOZOBASE Tsukuba 2.
2023: for ZOZOBASE Tsukuba 3, the team did not start from scratch. They extended the model with equipment-related constraints, a larger facility network and allocation logic across multiple Tsukuba-area sites.
Takeaway: optimization became reusable decision infrastructure for rare, high-stakes events like new facility launches.
🎬 How the video tells it
#	Time	Scene	What happens
1	0:00	Title & team	Case title, course and team intro
2	0:14	Yuki's order	A late-night order in Tokyo: a denim jacket + sneakers
3	0:24	Meet ZOZO	The ZOZOBASE pipeline; new centres change capacity
4	0:43	The problem	Jacket in Narashino, sneakers in Tsukuba, so the truck goes on a road trip; the second villain is imbalance
5	1:06	Insight & model	Orders → shops → clusters; Decision / Objective / Constraints
6	1:33	Solver story	Slow LP relaxations → barrier vs simplex → the bottleneck is structural
7	1:53	The rewind	Same order, now one centre, one box, zero road trips
8	2:04	Results	Tsukuba 2 (2020) → model extended for Tsukuba 3 (2023)
9	2:16	Close	"Reusable decision infrastructure"
<p> <img src="docs/images/order.jpg" width="49%" alt="Yuki places an order"> <img src="docs/images/problem.jpg" width="49%" alt="The inter-centre road trip"> <img src="docs/images/model.jpg" width="49%" alt="Shop clustering and the model"> <img src="docs/images/rewind.jpg" width="49%" alt="One centre, one box"> </p>

Note: Yuki, the shop names, and all on-screen counts and percentages are illustrative. The case does not publish ZOZO's actual data. Every factual statement in the narration comes from the case study.

🛠️ How it was made

Every frame is drawn in Python, with no video editor and no stock footage.

Part	Tool
Animation (1920×1080, 30 fps)	skia-python vector drawing, custom easing and characters
Voiceover	Kokoro-82M neural TTS via kokoro-onnx, run locally (voice af_heart)
Sound effects & music	Synthesised in NumPy (pops, whooshes, sad trombone, a marimba loop) with music ducked under the voice
Encoding	FFmpeg (H.264 + AAC)
Font	Inter (SIL Open Font License)
Repository structure
.
├── video/
│   └── ZOZO_Life_of_One_Order.mp4   # final video
├── docs/
│   ├── voiceover-script.md          # timestamped narration
│   └── images/                      # stills used in this README
├── src/
│   ├── script.py      # narration text + pronunciation respellings, per scene
│   ├── make_vo.py     # AI voiceover -> build/vo/*.wav + timing.json
│   ├── gfx.py         # palette, easing, drawing helpers, characters (Yuki, trucks, warehouses)
│   ├── scenes.py      # the 9 animated scenes + their sound-effect cues
│   ├── render.py      # renders stills or full scenes to MP4
│   └── audio.py       # synthesised SFX + music, mixed with the voice
├── models/README.md   # where to put the voice model files
├── build.sh           # one command to rebuild the video
├── requirements.txt
└── LICENSE
Rebuild it yourself

Requirements: Python 3.10+, FFmpeg, and the Inter font.

bash
# 1. Install Python packages
pip install -r requirements.txt

# 2. Get the voice model (see models/README.md)
#    -> models/kokoro-v1.0.onnx and models/voices-v1.0.bin

# 3. Install the Inter font (static OTFs), or put Inter-*.otf files in ./fonts
#    or set: export INTER_FONT_DIR=/path/to/inter/otf

# 4. Build (about 5–10 minutes on a laptop)
./build.sh

To change a line of narration, edit src/script.py and run ./build.sh again; the animation timing follows the voice automatically. To preview a single frame:

bash
python3 src/make_vo.py                 # once, to create timing data
python3 src/render.py still insight 26.5   # -> build/stills/insight_26.50.png
📚 Source & disclaimer
Case study: ZOZO Research: Optimizing Inventory Allocation for Scalable E-Commerce Logistics, Gurobi Optimization. Available on Gurobi's case studies page.
ZOZO Research: https://research.zozo.com/

This is an independent academic project created for coursework. It is not affiliated with or endorsed by ZOZO, Inc. or Gurobi Optimization. ZOZO, ZOZOTOWN, ZOZOBASE and Gurobi are trademarks of their respective owners. The original case study PDF is not redistributed here.

Code is released under the MIT License.
