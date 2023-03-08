 # The Open Building Analytics Working Group
 The OBA-WG is made up of practitioners in the building and energy data operations sector. The group is focused on developing a common set of open standards for building analytics. The goal is to enable the development of an interoperable set of tools and services that can be used by building owners, operators, and service providers to improve the performance of their buildings.

One of the first products of the OBA-WG is the [Open-FDD Repo](https://github.com/bbartling/open-fdd), a collection of fault detection and diagnostics (FDD) algorithms that can be used to detect anomalies in building systems. The algorithms are written in Python and are implemented around the ASHRAE Guideline 36 Fault Detection definitions.

The next goal for the working group is defining an analytic rule interface, which will allow sharing of analytic rules across different platforms and system architectures. Below is a straw-man definition of this interface.

Initially we will define these in python, as the python ecosystem brings the richest set of data science tools and is most widely supported in edge and cloud compute environments. Future work might include wrappers for R, Julia, or even a WebAssembly (WASM) implementation.

Assumptions will not be made about ontologies, data models, or streaming vs batch processing.

# Straw Man Interface:
Each analytic will be a python module that defines the `run_analysis` and the `generate_sample_config` functions with the following signatures:
```def run_analysis(data_df: pd.DataFrame, params: dict, output_col: str) -> pd.DataFrame:```
```def generate_sample_config() -> dict:```

A sample config might look like:
```yaml
name: "Rule 1"
description: "Rule 1 description"
version: "1.0"
  input:
    col_name_one: "datapoint_path_or_uuid"
    col_name_two: "datapoint_path_or_uuid"
    col_name_three: "datapoint_path_or_uuid"
    output_col: "equip_two_rule_one"
    params:
      param1: 1.0
      param2: 2.0
```

This method takes a Pandas data frame with columns named as defined in the  