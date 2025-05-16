# NumPy and Pandas fundamentals for handling biological datasets

:::{prereq}

* Programming Fundamentals in Python
  * Basic Python syntax and data structures
  * Functions and control flow
  * File handling in Python
  * Experience with Python IDEs and Jupyter notebooks
* Basic Biology Knowledge
  * Basic genomics terminology
  * Familiarity with common bioinformatics file formats (FASTA, FASTQ)
:::

## Who is the course for?

Bioinformaticians and genomics researchers who want to enhance their data analysis capabilities by mastering NumPy and Pandas for efficient processing of genomic datasets

## About the course

### Overall Course Objective

By the end of this course, students will be able to effectively utilize NumPy and Pandas libraries to manipulate, analyze, and process complex numerical and tabular data in Python, demonstrating proficiency in advanced array operations, data structures, and data manipulation techniques. Additionally, students will apply these skills to real-world bioinformatics problems, gaining practical experience in genomics data analysis and handling.

### Specific Learning Objectives

1. After completing the NumPy section and hands-on exercises, students will be able to:
   * Explain the purpose and advantages of using NumPy in scientific computing and data analysis
   * Create, manipulate, and efficiently implement NumPy arrays through advanced techniques including indexing, sorting, splitting, vectorized operations, and broadcasting
2. After completing the Pandas section and hands-on exercises, students will be able to:
   * Understand the relationship between Pandas and NumPy, and effectively use Pandas Series and DataFrames for data analysis
   * Perform advanced data manipulation techniques including indexing, filtering, handling missing data, and combining DataFrames through merging and concatenation

### Overall time schedule

```{csv-table}
:delim: ;
:widths: auto

Numpy for Bioinformatics ; 3 Hours
Pandas for Bioinformatics ; 3 Hours 
```

```{toctree}
:caption: Numpy for handling biological datasets 
:maxdepth: 1

0.Numpy_for_bioinformatics.md
1.numpy_intro.md
2.NumPy_Data_Types.md
3.Indexing_and_Slicing.md
4.Advance_indexing_filtering.md
5.Essential_array_operations.md
6.Vectorized_Operations_in_NumPy.md
6.1.Numpy_hands_on.ipynb
```

```{toctree}
:caption: Pandas for handling biological datasets 
:maxdepth: 1

7.Pandas_lesson plan.md
8.Introduction_to_pandas.md
9.Pandas_data_import_export.md
10.DataFrame_Manipulation.md
11.Pandas_indexing_slicing.md
12.Handling_Missing_Data.md
13.Merging_DataFrames.md
14.Pandas_summary_stats.md
15.Hands-on_expression_count_analysis.ipynb
```

## Datasets

* [Download Test dataset 1: Sample_group_info.csv](test_data/Sample_group_info.csv)

* [count_matrix.csv](test_data/count_matrix.csv)

## Dependencies

* All Python dependencies are listed in the `requirements.txt` file
* [Download requirements.txt](test_data/requirements.txt)

### Setup Python environment

1. Install Python3
2. Create a work-folder for the course exercises and hands-on sessions (e.g. `biont_module1`)
3. Move the `biont_module1` workfolder and download the `requirements.txt` file
4. Follow steps below

```bash
# work-folder: ~/playground/biont_module1

# Create Python environment (use python v.3.11 or above)
python -m venv venv

# Activate Python environment
source venv/bin/activate

# Upgrade pip (not mandatory)
pip install --upgrade pip

# Install dependencies
pip install -r requirements.txt
```

## Credits

* [BioNT - The Bio Network for Training](https://biont-training.eu/)
* [Norwegian AI Cloud](https://www.naic.no)
* [Scientific Computing Services, Department Informatics, University of Oslo](https://www.usit.uio.no/english/about/organisation/rde/scs/)
