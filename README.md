Link: https://jpk2003.github.io/dot_plot_generator/


# Dot Plot Generator

A standalone, browser-based tool for creating dot plot visualizations to compare survey data, typically between a current and a previous wave. The tool generates a plot showing the mean score for selected variables, their 95% confidence intervals, and an optional shadow plot of the previous wave's data for comparison.

This tool is a single HTML file that runs entirely in your browser. No internet connection, server, or installation is required.

## Features

- **Dual CSV Upload**: Load separate CSV files for your **Current Wave** and **Previous Wave** data.
- **Dynamic Variable Selection**: Once a CSV is loaded, variable dropdowns are populated with the column headers from your file, allowing for easy selection.
- **Automatic Stats Calculation**: The tool automatically computes the mean, standard deviation, and 95% confidence interval margin of error for each selected variable.
- **Previous Wave Auto-Matching**: When both current and previous wave CSVs are loaded, the tool automatically matches variables by name, populating the previous wave data for instant comparison.
- **Interactive Plotting**: The dot plot preview updates in real-time as you select variables and adjust settings.
- **Statistical Significance Testing**: Automatically runs a two-sample z-test to compare current and previous means, displaying a colored asterisk (green for increase, red for decrease) for statistically significant differences (p < .05).
- **Rich Customization**: Control the chart title, goal line value, axis widths, row heights, and legend visibility.
- **Manual Override**: All automatically calculated fields (Mean, ±, Prev Mean, Prev ±) are editable for manual adjustments or one-off plots.
- **Export Options**: Export the final dot plot as a high-quality **SVG** (vector) or **PNG** (raster) image.

## How to Use

### 1. Opening the Tool

Simply double-click the `DotPlotGenerator.html` file to open it in any modern web browser like Chrome, Firefox, Safari, or Edge.

### 2. Loading Data

The tool has two upload areas at the top:

- **Current Wave CSV**: Click or drag-and-drop your primary dataset here. This is the data that will be used to generate the main colored dots.
- **Previous Wave CSV**: (Optional) Click or drag-and-drop your comparison dataset here (e.g., from a previous survey). This data is used for the grey shadow plots.

Once a file is loaded, its name, column count, and row count will appear in the upload box.

### 3. Selecting Variables

After loading the **Current Wave CSV**, the `VARIABLE` column in each row below will transform into a dropdown menu.

1.  Click the dropdown in the first variable row.
2.  Select a variable from the list (e.g., "B: Satisfaction").
3.  The **Mean** and **±** (margin of error) fields will automatically populate based on the data in that column.

If you also loaded a **Previous Wave CSV**:

1.  Check the `Prev` box for that row.
2.  A new `PREV VARIABLE` dropdown will appear on the far right.
3.  If a variable with the same name exists in the previous CSV, it will be **auto-selected**, and the **Prev Mean** and **Prev ±** fields will auto-populate.
4.  You can also manually select a different variable from the `PREV VARIABLE` dropdown to compare two differently named variables.

### 4. Customizing the Chart

Use the controls at the top to customize the plot's appearance:

- **Chart Title**: Enter a title for your plot.
- **Goal**: Toggle the vertical goal line between 3.5 and 4.0.
- **Previous Mean Legend**: Change the legend text for the grey shadow dots (e.g., to a specific build version).
- **Show Legend**: Toggle the entire legend block on or off (defaults to off).
- **X-Axis Width / Row Height**: Use the sliders to expand or contract the plot dimensions for better readability or to fit more variables.

### 5. Interpreting the Plot

- **Colored Dots**: Represent the mean of the **current wave** data.
    - **Green**: The 95% confidence interval is entirely **above** the goal line.
    - **Yellow**: The 95% confidence interval **crosses** the goal line.
    - **Red**: The 95% confidence interval is entirely **below** the goal line.
- **Grey Shadow Dots**: Represent the mean of the **previous wave** data. The value is printed below the dot.
- **Confidence Intervals (CI)**: The horizontal "whisker" lines show the 95% CI for each mean.
- **Asterisks (*)**: A colored asterisk appears to the right of a dot if the difference between the current and previous mean is statistically significant (p < .05).
    - **Green Asterisk**: Significant increase.
    - **Red Asterisk**: Significant decrease.

### 6. Exporting Your Plot

Once you are satisfied with the preview, click the **Export SVG** or **Export PNG** button to download the chart to your computer. The filename will default to your chart title.

## Advanced Features

### Manual Data Entry

You can use the tool without loading any CSV files. Simply type your variable names, means, and margins directly into the input boxes in each row.

### Paste from Spreadsheet

For quickly populating the tool from Excel or Google Sheets:

1.  Click the **📋 Paste from Spreadsheet** button.
2.  In your spreadsheet, copy a block of cells with the following columns:
    - `Name`
    - `Mean`
    - `±`
    - `Prev Mean` (optional)
    - `Prev ±` (optional)
3.  Paste the data into the text area in the modal.
4.  Click **Import** to load the data into the variable rows.

## Technical Details

- **Technology**: The tool is built with vanilla HTML, CSS, and JavaScript. It has no external dependencies and runs completely offline.
- **Statistical Test**: The significance indicator uses a standard **two-sample z-test** for the difference between two means. The standard error for each mean is derived from the provided 95% confidence interval margin of error (`SE = Margin / 1.96`).
