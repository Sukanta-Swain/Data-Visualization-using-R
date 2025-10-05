# Data-Visualization-using-R



 **complete teaching blueprint** with 3 parts:
1️⃣ **Prerequisites**
2️⃣ **Topics to Cover (Structured Curriculum)**
3️⃣ **Detailed Notes and Teaching Guidance**

---

## 🧩 1. Prerequisites

Before starting visualization, learners should already know:

| Area                      | Key Skills / Functions                                               | Example / Practice          |
| ------------------------- | -------------------------------------------------------------------- | --------------------------- |
| **Basic R Syntax**        | Assignments (`<-`), vectors, lists, factors                          | `x <- c(1,2,3)`             |
| **Data Frames & Tibbles** | Create, import (`read.csv()`, `readxl`), inspect (`head()`, `str()`) | Load CSV file and preview   |
| **Packages**              | Installing and loading (`install.packages()`, `library()`)           | `library(ggplot2)`          |
| **Basic Statistics**      | Mean, median, frequency                                              | `mean(data$age)`            |
| **Basic Data Cleaning**   | Handling NAs, filtering, transforming                                | `na.omit()`, `subset()`     |
| **Basic plotting**        | `plot()` function in Base R                                          | `plot(x, y)` simple scatter |

🧠 *Optional but helpful*: Familiarity with `dplyr`, `tidyr`, and the “tidyverse” philosophy.

---

## 🎨 2. Topics to Cover (Structured Curriculum)

You can divide the visualization module into **6 parts (from basic to advanced)**:

| Part                                           | Topics                                                                                                                                                | Tools / Packages                                | Example Visualization     |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- | ------------------------- |
| **1. Introduction to Data Visualization**      | - Purpose of visualization<br>- Grammar of graphics concept<br>- When to use which chart                                                              | Base R, ggplot2                                 | Concept slides + examples |
| **2. Base R Graphics**                         | - `plot()`, `barplot()`, `hist()`, `boxplot()`, `pie()`<br>- Customization (titles, axes, colors, legends)                                            | Base R                                          | `hist(mtcars$mpg)`        |
| **3. ggplot2 Essentials**                      | - ggplot syntax: `ggplot(data) + geom_*()`<br>- Aesthetic mappings (`aes()`)<br>- Common geoms: `geom_point`, `geom_bar`, `geom_line`, `geom_boxplot` | `ggplot2`                                       | Scatter, line, bar        |
| **4. Advanced ggplot Customization**           | - Themes (`theme_minimal`, `theme_classic`)<br>- Scales (`scale_fill_manual`, `scale_color_gradient`)<br>- Faceting (`facet_wrap`, `facet_grid`)      | `ggplot2`, `ggthemes`                           | Multi-panel plot          |
| **5. Data Visualization for Analysis**         | - Correlation plots<br>- Distribution plots<br>- Time series visualization<br>- Heatmaps                                                              | `corrplot`, `ggcorrplot`, `plotly`, `lubridate` | Correlation matrix        |
| **6. Interactive & Specialized Visualization** | - Interactive charts with `plotly`, `highcharter`<br>- Maps with `ggmap`, `sf`<br>- Dashboards using `shiny`                                          | `plotly`, `leaflet`, `sf`, `shiny`              | Interactive map/dashboard |

---

## 🧾 3. Detailed Notes and Teaching Guidance

Here’s how you can deliver each module:

---

### **📘 Module 1: Introduction to Data Visualization**

**Concepts:**

* Purpose: communicate insights effectively.
* Types: Exploratory (understand data) vs Explanatory (communicate findings).
* Grammar of Graphics (data → aesthetics → geometries → stats → scales → theme).

**Example:**

```R
library(ggplot2)
ggplot(mtcars, aes(x=wt, y=mpg)) + geom_point()
```

🗒️ *Explain the mapping of data to visual elements.*

---

### **📘 Module 2: Base R Visualization**

**Functions:**

* `plot()` – scatter, line plots
* `barplot()`
* `hist()`
* `boxplot()`
* `pie()`

**Example:**

```R
barplot(table(mtcars$cyl), main="Car Cylinders", col="lightblue")
```

🗒️ *Focus on parameters like `main`, `xlab`, `ylab`, `col`, `pch`, `lwd`.*

---

### **📘 Module 3: ggplot2 Fundamentals**

**Core Concepts:**

* Data → Aesthetics → Geometries
* Layering concept with `+`

**Example:**

```R
ggplot(mtcars, aes(x=wt, y=mpg, color=factor(cyl))) +
  geom_point(size=3) +
  labs(title="MPG vs Weight by Cylinders")
```

🗒️ *Demonstrate how color encodes category and how ggplot handles layering.*

---

### **📘 Module 4: ggplot Customization**

**Concepts:**

* Themes: `theme_bw()`, `theme_minimal()`
* Labels: `labs()`
* Legends: `guides()`
* Facets: `facet_wrap(~cyl)`

**Example:**

```R
ggplot(mtcars, aes(wt, mpg)) +
  geom_point(aes(color=factor(gear))) +
  facet_wrap(~gear) +
  theme_minimal() +
  labs(title="MPG vs Weight by Gear")
```

🗒️ *Teach how to modify the overall look and layout.*

---

### **📘 Module 5: Analytical Visualizations**

**Concepts:**

* Correlation plot
* Distribution (density, histogram)
* Time series (line charts)
* Boxplots for spread
* Heatmaps

**Examples:**

```R
library(corrplot)
corrplot(cor(mtcars), method="circle")

ggplot(iris, aes(Sepal.Length, fill=Species)) + geom_density(alpha=0.6)
```

🗒️ *Focus on using visualizations for insights.*

---

### **📘 Module 6: Interactive & Specialized Plots**

**Concepts:**

* Convert ggplot → plotly
* Geographic visualization (`sf`, `leaflet`)
* Basic `shiny` dashboard for visual display

**Examples:**

```R
library(plotly)
p <- ggplot(mtcars, aes(wt, mpg)) + geom_point()
ggplotly(p)
```

🗒️ *Highlight how interactivity helps in dashboards.*

---

## 🧭 Optional Add-ons (for advanced learners)

| Area                      | Package                  | Example                      |
| ------------------------- | ------------------------ | ---------------------------- |
| **Time series**           | `ggfortify`, `dygraphs`  | Line charts with date axis   |
| **Network graphs**        | `igraph`, `ggraph`       | Social network visualization |
| **3D plots**              | `plotly`, `rgl`          | Interactive 3D scatter plots |
| **Dashboard integration** | `shiny`, `flexdashboard` | Combine plots into dashboard |

---


Let’s go through this **comprehensively**, grouping them by their **visualization purpose** and **use case**.

---

## 🎯 1. **General & Grammar-of-Graphics Frameworks**

| Package                             | Purpose                                                | Key Highlights / Example                                       |
| ----------------------------------- | ------------------------------------------------------ | -------------------------------------------------------------- |
| **ggplot2**                         | Foundation of modern R visualization                   | Grammar of Graphics; static but highly customizable.           |
| **lattice**                         | Traditional multi-panel plotting                       | Elegant for conditioning plots (like Trellis).                 |
| **base R graphics**                 | Built-in plotting system                               | Quick, procedural plots using `plot()`, `hist()`.              |
| **ggvis**                           | Interactive Grammar of Graphics (successor to ggplot2) | Similar syntax to ggplot2, supports interactivity via `shiny`. |
| **cowplot / patchwork / gridExtra** | Layout and combination of multiple ggplots             | Combine multiple plots for publication-style visuals.          |

**Example (patchwork):**

```R
library(ggplot2)
library(patchwork)
p1 <- ggplot(mtcars, aes(wt, mpg)) + geom_point()
p2 <- ggplot(mtcars, aes(factor(cyl), mpg)) + geom_boxplot()
p1 + p2
```

---

## 🌈 2. **Data Exploration and Analytics Visualization**

| Package                   | Purpose                                         | Key Highlights                                       |
| ------------------------- | ----------------------------------------------- | ---------------------------------------------------- |
| **DataExplorer**          | Automated EDA visualization                     | One-line command for dataset overview.               |
| **GGally**                | Extensions to ggplot2 (correlation, pair plots) | Useful for pairwise relationships (`ggpairs`).       |
| **corrplot / ggcorrplot** | Correlation heatmaps                            | Attractive visualization of correlation matrices.    |
| **VIM**                   | Visualize missing values                        | Plot NA patterns.                                    |
| **Hmisc**                 | High-level functions for data description       | Includes specialized summary plots.                  |
| **inspectdf**             | Visual comparison of multiple data frames       | Colorful bar plots comparing variable distributions. |
| **PerformanceAnalytics**  | Financial return analysis visualizations        | Scatter matrix, density, correlation.                |

**Example:**

```R
library(GGally)
ggpairs(iris, aes(color = Species))
```

---

## 📊 3. **Interactive Visualization**

| Package         | Purpose                                                    | Key Features                                      |
| --------------- | ---------------------------------------------------------- | ------------------------------------------------- |
| **plotly**      | Interactive charts (built on JavaScript library Plotly.js) | Convert ggplot2 to interactive with `ggplotly()`. |
| **highcharter** | R interface to Highcharts JS                               | Stunning, professional interactive charts.        |
| **dygraphs**    | Interactive time-series visualization                      | Great for zooming/panning series.                 |
| **echarts4r**   | R interface to Apache ECharts                              | High-performance interactive visuals.             |
| **rbokeh**      | Interactive plots (Python Bokeh style)                     | Ideal for dashboards and exploration.             |
| **visNetwork**  | Interactive network/graph visualization                    | Drag, zoom, click interactions.                   |
| **leaflet**     | Interactive maps (geospatial visualization)                | Build interactive map layers easily.              |

**Example:**

```R
library(plotly)
p <- ggplot(mtcars, aes(wt, mpg, color=factor(cyl))) + geom_point()
ggplotly(p)
```

---

## 🗺️ 4. **Geospatial Visualization**

| Package                                  | Purpose                                       | Key Features                                |
| ---------------------------------------- | --------------------------------------------- | ------------------------------------------- |
| **sf (simple features)**                 | Handling and plotting spatial data            | Core geospatial data format in modern R.    |
| **tmap**                                 | Thematic mapping (static + interactive)       | `tm_shape() + tm_polygons()` syntax.        |
| **leaflet**                              | Interactive mapping                           | Pan/zoom maps with markers and layers.      |
| **ggmap**                                | Combines ggplot2 with Google Maps backgrounds | Overlay data on real-world maps.            |
| **rnaturalearth / rworldmap / maptools** | Provides map data for countries and regions   | Easy plotting of administrative boundaries. |
| **cartography**                          | Advanced cartographic visualizations          | Choropleths, proportional symbols, etc.     |

**Example:**

```R
library(tmap)
data(World)
tm_shape(World) + tm_polygons("pop_est", palette="viridis", title="Population")
```

---

## 🕒 5. **Time-Series Visualization**

| Package                   | Purpose                                    | Key Features                                    |
| ------------------------- | ------------------------------------------ | ----------------------------------------------- |
| **ggfortify**             | Auto-plot for time-series, PCA, clustering | Use `autoplot()` for quick visuals.             |
| **dygraphs**              | Interactive time-series charts             | Zoom and hover interactions.                    |
| **tsibble**               | Tidyverse-style time-series data           | Used with `feasts` and `fable` for forecasting. |
| **ggseas / ggTimeSeries** | Seasonality and time plots with ggplot2    | Useful for decomposed trend analysis.           |
| **lubridate + ggplot2**   | Simplify date-time handling                | Combine for dynamic time-based plots.           |

**Example:**

```R
library(ggfortify)
autoplot(AirPassengers) + ggtitle("Monthly Airline Passengers")
```

---

## 🧭 6. **Network and Relationship Visualization**

| Package        | Purpose                                    | Key Features                          |
| -------------- | ------------------------------------------ | ------------------------------------- |
| **igraph**     | Create and visualize network graphs        | Social networks, dependencies.        |
| **ggraph**     | Grammar-of-graphics for networks           | Works like ggplot2 for graph objects. |
| **networkD3**  | Interactive D3-based network visualization | Sankey, force, tree diagrams.         |
| **DiagrammeR** | Flowcharts and graph diagrams              | Visualize pipelines and workflows.    |

**Example:**

```R
library(igraph)
g <- make_ring(10)
plot(g)
```

---

## 📈 7. **Dashboard & Reporting**

| Package                      | Purpose                           | Key Features                            |
| ---------------------------- | --------------------------------- | --------------------------------------- |
| **shiny**                    | Interactive web apps & dashboards | Real-time updates, user input handling. |
| **flexdashboard**            | Turn R Markdown into dashboards   | Easy layout definition.                 |
| **shinydashboard / bs4Dash** | Prebuilt dashboard templates      | Clean UI and navigation.                |
| **shinyWidgets**             | Enhanced shiny UI components      | Toggle buttons, sliders, progress bars. |
| **RMarkdown + knitr**        | Integrate visuals into reports    | Reproducible data storytelling.         |

**Example:**

```R
library(flexdashboard)
# --- YAML Header Example ---
# title: "Sales Dashboard"
# output: flexdashboard::flex_dashboard
```

---

## 📦 8. **Specialized Visualization**

| Package                    | Domain                     | Visualization Type                        |
| -------------------------- | -------------------------- | ----------------------------------------- |
| **waffle / ggwaffle**      | Infographics               | Waffle charts for proportions             |
| **treemap / treemapify**   | Hierarchical data          | Tree and nested box visualization         |
| **wordcloud / wordcloud2** | Text data                  | Frequency clouds for words                |
| **UpSetR**                 | Intersection visualization | Alternative to Venn diagrams              |
| **VennDiagram / ggvenn**   | Set intersections          | Traditional Venn visualization            |
| **gganimate**              | Animation                  | Animated transitions in ggplot            |
| **ggridges**               | Distribution visualization | Ridgeline plots for overlapping densities |
| **ggtext / ggrepel**       | Label and text enhancement | Improves readability in dense charts      |
| **ggthemes**               | Visual themes              | Apply presentation or publication themes  |

**Example:**

```R
library(gganimate)
p <- ggplot(gapminder, aes(gdpPercap, lifeExp, size=pop, color=continent)) +
  geom_point(alpha=0.7) +
  scale_x_log10() +
  labs(title="Year: {frame_time}") +
  transition_time(year)
animate(p)
```

---

## 🧠 9. **Comprehensive “Power Toolkit” Recommendation**

If you want to teach **a practical, modern visualization toolkit**, focus on:

| Category                    | Primary Packages                     |
| --------------------------- | ------------------------------------ |
| **Static Graphics**         | `ggplot2`, `ggthemes`, `patchwork`   |
| **Interactive Visuals**     | `plotly`, `highcharter`, `echarts4r` |
| **Geospatial**              | `sf`, `tmap`, `leaflet`              |
| **Time Series**             | `ggfortify`, `dygraphs`              |
| **EDA / Correlation**       | `GGally`, `corrplot`, `DataExplorer` |
| **Dashboards**              | `shiny`, `flexdashboard`             |
| **Animated / Storytelling** | `gganimate`, `ggridges`              |

---
https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-r-visuals



