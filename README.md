# UMARV Hardware

PCB designs and hardware files for the University of Michigan Autonomous Robotic Vehicle (UMARV) project.

> **For CS/software folks:** You probably just need to browse a schematic or check a pinout. Jump to the folder for your board below and open the `README.md` inside it — no Git setup needed, GitHub renders schematics and PDFs in the browser.

---

## Repo Structure

```
embedded_hardware/
├── estop-lora-esp32/        # Remote E-stop board (LoRa + ESP32)
│   ├── schematic.SchDoc
│   ├── board.PcbDoc
│   ├── Project Outputs/     #includes Gerber(.GM, .GBL, etc), DRC, Pick and Place files
│   └── README.md            # Pinout, ROS2 topic links, revision history
├── power-distribution/
├── motor-driver/
├── coming-soon/
├── .gitignore
└── README.md                # (this file)
```

Each board folder should have its own `README.md` explaining or linking to: 
- What the board does
- Which ROS2 topics / signals it connects to
- Connector pinout

---

## First-Time Setup (Hardware Contributors)

You need to be a member of the `umigv` GitHub org first. 

### Clone only your board (recommended — avoids downloading large files from other boards)

```bash
git clone --no-checkout https://github.com/umigv/embedded_hardware
cd hardware
git sparse-checkout init --cone
git sparse-checkout set your-board-folder-name
git checkout main
```

Replace `your-board-folder-name` with the actual folder, e.g. `estop-lora-esp32`.
- Naming convention: `function-component`

### Clone everything

```bash
git clone https://github.com/umigv/hardware
cd hardware
```

---

## Pushing a New Board

### 1. If you cloned with sparse checkout, add your folder to the sparse list first

```bash
git sparse-checkout add your-new-board-name
```

### 2. Create your folder and add files

```bash
mkdir your-new-board-name
cd your-new-board-name
# Copy your Altium files in here
```

### 3. Commit and push

```bash
git add your-new-board-name/
git commit -m "your-new-board-name: initial upload rev1"
git push
```

---

## Pushing Updates to an Existing Board

```bash
cd hardware/your-board-folder
# make your changes
git add .
git commit -m "your-board-name: describe what changed (e.g. fix antenna footprint)"
git push
```

Keep commit messages descriptive — future you will thank you.

---

## Altium-Specific Notes

- check root .gitignore file for what it ignores
- individual folder .gitignores can be set to more specific, but cannot include what the root ignores 

- **Include:** `.SchDoc`, `.PcbDoc`, `.PrjPcb`, `gerbers/`, BOM export, project-specific libraries
- **Do not include:** `History/`, `__Previews/`, `ProjectLogs/` — these are auto-generated and handled by `.gitignore`
- If you use a shared library, document the library name and version in your board's `README.md` so others can open it cleanly
