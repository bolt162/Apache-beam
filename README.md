# Apache Beam Features Colab Assignment README

This repository contains an Apache Beam Google Colab notebook demonstrating key data processing concepts and transforms as required for the assignment.

---

## Assignment Goal

The goal of this assignment is to build and demonstrate an Apache Beam data processing pipeline that showcases the use of fundamental and advanced transforms, illustrating its capabilities for both batch and stream processing concepts.

The demonstration is provided in the Jupyter/Colab notebook: **`Getting_started_Tour_of_Beam.ipynb`**.

---

## Features Demonstrated

The following required Apache Beam features are implemented and demonstrated in the submitted Colab notebook:

| Feature | Apache Beam Transform/Concept | Implemented in Notebook |
| :--- | :--- | :--- |
| **Composite Transform** | Custom `beam.PTransform` subclass | Yes |
| **Pipeline I/O** | `beam.io.ReadFromText`, `beam.io.WriteToText`, `beam.Create` | Yes |
| **ParDo** | `beam.ParDo` (with custom `DoFn`) | Yes |
| **Windowing** | `beam.WindowInto` (e.g., `FixedWindows`) | Yes |
| **Map** | `beam.Map` | Yes |
| **Filter** | `beam.Filter` | Yes |
| **Partition** | `beam.Partition` | Yes |

---

## Code Walkthrough and Execution Explanation

The Colab notebook implements a complete data pipeline (e.g., a data cleaning or categorization task) to showcase the required features.

### 1. Pipeline Setup and I/O

The pipeline starts by initializing the `beam.Pipeline` object:

* **Input (Pipeline I/O):** Data is read into a **PCollection** using `beam.Create` for demonstration with a small, in-memory dataset, or **`beam.io.ReadFromText`** for file-based batch processing.
* **Output (Pipeline I/O):** The final processed **PCollection** is written to a sink using `| beam.io.WriteToText('output_results.txt')`.

### 2. Core Element-wise Transforms

These transforms demonstrate fundamental data manipulation:

* **`Map`:** A basic `beam.Map` is used for **one-to-one transformations** (e.g., standardizing text case or extracting a single field).
* **`Filter`:** The `beam.Filter` transform is applied to **selectively keep elements** that meet a specific Boolean condition (e.g., excluding invalid records).
* **`ParDo` (Parallel Do):** The most general and powerful transform. A custom `beam.DoFn` is defined and applied using `| beam.ParDo(CustomDoFn())` to demonstrate complex, stateful, or **many-to-many logic**.

### 3. Data Flow and Reusability

These features manage control flow and code structure:

* **`Partition`:** The `| beam.Partition(num_partitions, partition_fn)` transform is used to **split the main PCollection** into two or more distinct, non-overlapping PCollections based on a function (e.g., separating records into 'Valid' and 'Error' streams).
* **`Composite Transform`:** A custom class inheriting from **`beam.PTransform`** is created. This encapsulates a reusable sequence of several lower-level transforms (like `Map` followed by `GroupByKey`) into a single, clean, and well-named step, such as `| 'Calculate Final Score' >> CalculateFinalScore()`.

### 4. Handling Time-Series Data

* **`Windowing`:** The `| beam.WindowInto(window.FixedWindows(60))` transform is applied to demonstrate how Beam groups elements into **time-based windows** (e.g., 60-second intervals). This is a conceptual demonstration essential for correctly aggregating data that arrives continuously in a streaming pipeline.

---

## Execution and Walkthrough Video

https://drive.google.com/file/d/14Bdfd30_bI7x0gC0KydAvAMsNxmJld3H/view?usp=drive_link

A code walkthrough video is submitted alongside this README. The video explains the following:

1.  **Inputs:** Defines the source data (either hard-coded or from a file) used to execute the pipeline in the Colab notebook.
2.  **Execution:** Steps through the Colab notebook, executing each cell and pausing to explain the transformation occurring at each stage (e.g., what the `Map` transform does, how `Filter` removes records).
3.  **Outputs:** Highlights the final processed data, demonstrating the results of the full pipeline execution and confirming the output of key transforms like `Partition` and the final I/O sink.
