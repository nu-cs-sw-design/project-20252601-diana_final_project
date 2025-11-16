# Project: Kniting Visualizer

## Contributors
Diana Whealan

## Dependencies
- LANGUAGE AND VERSION
- EXTERNAL LIBRARIES
- ETC

## Build Instructions
HOW TO BUILD YOUR PROJECT.

# Knitting Pattern Visualization Project

This project generates visual representations of knitting patterns by parsing pattern instructions and creating interactive charts.

## Code Entry Points

The main entry point for the application is:

- **`engine/main.py`** - Main script that creates chart sections, processes knitting patterns, and exports JSON data for visualization.

To run the application:
cd engine
python main.py## Example Usage

The `main.py` file contains a complete example demonstrating how to create and configure chart sections. Here's a simplified version:

from chart_section import ChartSection
import json

if __name__ == "__main__":
    chart_sections = []
    
    # Create a raglan chart section
    raglan = ChartSection(name="raglan", start_side="RS", sts=23, rows=21)
    raglan.cast_on_start(122)
    raglan.repeat_rounds(["repeat(k1, p1)"], 15)
    raglan.repeat_rounds(["repeat(k1)"], 30)
    raglan.place_marker("WS", 4)
    raglan.add_round("bo4, repeat(k1), rm").place_on_hold()
    # ... additional pattern instructions ...
    
    chart_sections.append(raglan)
    
    # Export to JSON
    charts_data = {
        "charts": [
            {
                "name": chart.name,
                "nodes": chart.nodes,
                "links": chart.links
            }
            for chart in chart_sections
        ]
    }
    
    with open("charts.json", "w") as f:
        json.dump(charts_data, f, indent=2)The example in `main.py` includes three chart sections:
- `raglan` - Front raglan section
- `raglan_back` - Back raglan section  
- `sleeve` - Sleeve section

## JSON Export Location

The application exports JSON data in two formats:

1. **Master file**: `charts.json` (in the `engine/` directory)
   - Contains all chart sections in a single file
   - Structure: `{"charts": [{"name": "...", "nodes": [...], "links": [...]}, ...]}`

2. **Individual chart files**: `{chart_name}.json` (in the `engine/` directory)
   - One file per chart section (e.g., `raglan.json`, `raglan_back.json`, `sleeve.json`)
   - Structure: `{"name": "...", "nodes": [...], "links": [...]}`

Both formats are written to the `engine/` directory when you run `main.py`.

## Visualizer HTML Location

The interactive visualizer is located at:

- **`visualizaion.html`** (root directory)

To use the visualizer:

1. Generate the JSON files by running `engine/main.py`
2. Open `visualizaion.html` in a web browser
3. The visualizer will automatically load `charts.json` from the `engine/` directory (or `engine2/charts.json` based on the current path configuration)

The visualizer provides:
- Interactive tabbed interface for multiple charts
- SVG rendering of knitting patterns with color-coded stitch types:
  - Blue (`k`) - Knit stitches
  - Purple (`p`) - Purl stitches
  - Green (`inc`) - Increases
  - Red (`dec`) - Decreases
- Download functionality for individual chart SVGs

## Project Structure

