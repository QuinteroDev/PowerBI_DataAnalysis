## Analysis of Service Level for Global Tech Solutions in 2020.

## Analyze the data

Upon initial exploration of the dataset provided by Global Tech Solutions, I identified details of delivery per line, including four columns of dates and information about locations, customers, delivery types, and organizational details. This dataset contained all the necessary elements to develop a service level dashboard focusing on timely versus delayed deliveries.

## Clean the data

I started by uploading the provided CSV file into PowerQuery, taking the following steps to prepare the data:

**Changed Type to Date**: I noticed discrepancies in date formats across several columns upon uploading. I removed the default formatting steps as I did not plan to aggregate these columns. I retained text formats for all columns except those containing dates, which I converted to Date format.

**Removed Columns**: To simplify the data model, I removed the "Sales Organization Category" as it was not relevant for my analysis and "Pick Date" due to its high percentage of null values and a 96% match with the "Planned Goods Issue" column.

**Customer Empty Filtered**: I encountered rows with "#value!" in both 'Sold to Customer' and 'Ship to Number' fields. I crafted a formula in M to exclude such rows since they lacked recognizable customer data for those shipments.

**ReplaceSold**: Several rows were marked as "#VALUE!" for the customer identified by the ship to number 39003699. Typically, I would verify customer details in an ERP system, but lacking access, I assumed 'Sold to Customer' is identical to 'Ship to Number' and set up a parameter with a default 'no' value to address any future occurrences of "#VALUE!".

**Change Name Columns**: Post-analysis, I renamed columns to "Actual Date Arrival" and "Estimated Date Arrival" for clarity. "Actual Good Issue Date" was retained for potential future analysis.

**Add Country Code Column**: I added a new column for country codes based on plant locations, using a formula to extract the first two letters from each shipping plant number. This column is essential as a foreign key linking to the newly created "Countries" table.

**Add Delivery Status**: I introduced a conditional column to compare "Actual Date Arrival" and "Estimated Date Arrival" statuses, which will support dashboard calculations.

**Remove Non-EMEA Countries**: I excluded locations outside the EMEA region, such as the USA.

Note: The "Group Code" column contains some blank rows; I left these untouched as they are not utilized for dashboard displays.

## Create Data Model

I renamed the source file to "FACT_deliveries" to designate it as the fact table.

I established "Countries" and "Incoterms" tables to group relevant columns, facilitating stakeholders' data access.

I formulated a "Dates" table using DAX's Calendar function, incorporating month names and numbers for sorting purposes within visualizations.

## Visualize results and analisis.

In the report view, I concealed columns not utilized to streamline the interface. I crafted five visualizations:

**Column Line Chart**: Displays the number of shipments and the percentage delivered on time throughout 2020, with tooltips guiding users for detailed monthly data exploration.

**Gauge**: Represents the percentage of on-time shipments with a neutral-colored KPI gauge, setting 95% as the benchmark.

**3 Cards**: Display the number of customers, shipments, and the top customer based on the shipment count under the current filter settings.

**Filters Instruction**: Filters are initially hidden; users can deploy them via arrows, selecting options like Country/Plant, Incoterms, and Delivery Type Code to tailor the data displayed.

**Measures Folder**: Contains three measures—'Delivered on Time', 'Target Service Level', and 'Top Customer Deliveries'—centralized for ease of access.

The dashboard's aesthetics are designed to be clean and professional, utilizing a corporate color scheme.

This analysis reveals varied performance across regions, with some showing lower delivery efficiencies, potentially due to the logistical challenges posed by the 2020 pandemic, suggesting a need for a comparative analysis with previous years.
