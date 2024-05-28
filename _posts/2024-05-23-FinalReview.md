---
comments: true
layout: post
title: Final Review
description: Full Stack Development 
type: plans
courses: {'compsci': {week: 35} }
---

# Overview 

In order to exhibit my skills as a full stack developer, I created a web application that filters and displays S&P 500 companies based on their founding dates. The backend, built with Flask and Flask-RESTful, processes date range queries, retrieves relevant company data from a preprocessed CSV file, and returns the filtered results. The frontend features an interactive user interface with a noUiSlider-powered date range selector, allowing users to dynamically display companies matching the selected criteria. This project demonstrates my proficiency in creating robust APIs, implementing efficient data processing, and developing responsive web interfaces.

# Backend Api

```python
def post(self):
    try:
        payload = request.get_json()  # Get JSON payload from the POST request
        print(f"Received payload: {payload}")  # Debugging line to print the payload
        if 'dates' not in payload or len(payload['dates']) != 2:
            return {'error': 'Start and end dates not provided'}, 400  # Return error if 'dates' are not in the payload

```

## Handling POST Requests

- Payload Retrieval: The post method fetches JSON data from the request.

- Payload Validation: Checks if the payload contains the 'dates' key and that it has exactly two dates.

## Date Conversion/Filtering/Formatting

```python
        # Convert date strings to years
        try:
            start_date = datetime.strptime(payload['dates'][0], '%Y-%m-%d').year
            end_date = datetime.strptime(payload['dates'][1], '%Y-%m-%d').year
        except ValueError as e:
            return {'error': f'Invalid date format: {str(e)}'}, 400  # Return error if date format is invalid

```

- String to Date Conversion: Attempts to convert the date strings to datetime objects and extracts the year.
 
- Error Handling: If the date format is incorrect, it returns a 400 Bad Request error.

```python
        # Get companies founded within the date range using the Stockfind model
        filtered_data = self.model.get_companies_by_date_range(start_date, end_date)

```

- The model's get_companies_by_date_range method is called to retrieve companies founded within the specified date range.

```python
        # Format the data as a list of dictionaries
        formatted_data = [
            {
                'Company Name': entry['Symbol'],
                'Founded': entry['Founded'],
                'GICS Sector': entry['GICS Sector']
            }
            for entry in filtered_data  # Iterate over the filtered data to format each entry
        ]

```

- Formatting: The filtered data is transformed into a list of dictionaries with keys: 'Company Name', 'Founded', and 'GICS Sector'.

- Same output should be seen when testing backend with postman after successful 200 request.

# Backend Model

## Initialization/Data Cleaning 

```python
def __init__(self):
    self.data = pd.read_csv('S&P500.csv')  # Read CSV file containing S&P 500 data
    self._clean()  # Clean the data after loading

```

- Reads through CSV file and cleans it using the _clean method.

- All under the Stockfind class, ensures only one instance of class exists.

- Similar to ML model implemented in previous projects

```python
def _clean(self):
    # Retain only the necessary columns
    required_columns = ['Symbol', 'Founded', 'GICS Sector']
    # Ensure columns exist in the CSV
    for col in required_columns:
        if col not in self.data.columns:
            raise ValueError(f"Column {col} not found in the CSV file")

    self.data = self.data[required_columns]  # Keep only the required columns
    
    # Extract earliest year if the 'Founded' field contains multiple years
    self.data['Founded'] = self.data['Founded'].apply(lambda x: int(re.search(r'\d{4}', str(x)).group(0)))
    # Convert 'Founded' column to numeric, invalid parsing will be set as NaN
    self.data['Founded'] = pd.to_numeric(self.data['Founded'], errors='coerce')

```

- Required Columns: Ensures that the CSV file contains the necessary columns: 'Symbol', 'Founded', and 'GICS Sector'.

- Extract Earliest Year: Uses a regular expression to extract the first four-digit year from the 'Founded' field.

- Convert to Numeric: Converts the 'Founded' column to numeric values

## Merge Sorting Algorithm

```python
def merge_sort(self, arr):
    # Recursive merge sort implementation to sort the array of dictionaries by 'Founded' key
    if len(arr) > 1:
        mid = len(arr) // 2  # Find the middle of the array
        left_half = arr[:mid]  # Split the array into left half
        right_half = arr[mid:]  # Split the array into right half

        self.merge_sort(left_half)  # Recursively sort the left half
        self.merge_sort(right_half)  # Recursively sort the right half

        i = j = k = 0  # Initialize indices for left half, right half, and main array
        # Merge the sorted halves back into the main array
        while i < len(left_half) and j < len(right_half):
            if left_half[i]['Founded'] < right_half[j]['Founded']:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        # Copy any remaining elements from the left half
        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        # Copy any remaining elements from the right half
        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1

```

- Merge Sort: Implements the merge sort algorithm to sort an array of dictionaries based on the 'Founded' key.

## Filter Companies Based on Date Range

```python
def get_companies_by_date_range(self, start_year, end_year):
    # Filter the data to get companies founded within the specified date range
    filtered_data = self.data[(self.data['Founded'] >= start_year) & (self.data['Founded'] <= end_year)]
    data_list = filtered_data.to_dict('records')
    self.merge_sort(data_list)  # Sort the list using merge sort
    return data_list

```

- Filtering: Filters the dataset to include companies founded within the specified date range.

- Convert to List of Dictionaries: Converts the filtered data to a list of dictionaries.

- Sort: Sorts the list using the merge_sort method.

# Backend Testing

![Postman](https://files.catbox.moe/8xlv8n.png)

- Postman with formatted JSON

![Payload](https://files.catbox.moe/nbyns2.png)

- Payload works and initializes a post request.

# Frontend

![Feature](https://files.catbox.moe/imly5o.png)

## Javascript 

```javascript
    document.addEventListener('DOMContentLoaded', function () {
        // Get references to the HTML elements
        const slider = document.getElementById('slider-range');
        const amount = document.getElementById('amount');
        const submitBtn = document.getElementById('submit');
        const dataBody = document.getElementById('dataBody');

        // Initialize the noUiSlider
        noUiSlider.create(slider, {
            start: [1900, 2024], // Initial values for the slider handles
            connect: true, // Connect the range between the handles
            range: {
                'min': 1800, // Minimum value for the slider
                'max': new Date().getFullYear() // Maximum value for the slider
            },
            step: 1, // Slider increments in steps of 1 year
            tooltips: true, // Show tooltips with the slider values
            format: {
                to: value => Math.round(value), // Round the slider values for display
                from: value => Number(value) // Convert the slider values from strings
            }
        });

        // Update the displayed date range when the slider values change
        slider.noUiSlider.on('update', function (values, handle) {
            amount.value = values.map(value => Math.round(value)).join(' - ');
        });

        // Event listener for the submit button
        submitBtn.addEventListener('click', function () {
            // Get the start and end year from the slider
            const startYear = slider.noUiSlider.get()[0];
            const endYear = slider.noUiSlider.get()[1];

            // Make a POST request to the API with the selected date range
            fetch('http://127.0.0.1:8008/api/found/filter', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    dates: [`${startYear}-01-01`, `${endYear}-12-31`] // Send the full date range
                })
            })
            .then(response => {
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                return response.json();
            })
            .then(data => {
                // Render the received data into the table
                renderData(data);
            })
            .catch(error => {
                console.error('Error fetching data:', error);
                alert('Error fetching data:', error);
            });

            // Function to render the data into the table
            function renderData(data) {
                dataBody.innerHTML = ''; // Clear previous data
                if (data.length === 0) {
                    dataBody.innerHTML = '<tr><td colspan="3">No companies found in this range.</td></tr>';
                } else {
                    // Create a new row for each company in the data
                    data.forEach(function (company) {
                        const row = document.createElement('tr');
                        row.innerHTML = `<td>${company['Company Name']}</td><td>${company['Founded']}</td><td>${company['GICS Sector']}</td>`;
                        dataBody.appendChild(row);
                    });
                }
            }
        });
    });

```

## Slider Initialization: Configures the noUiSlider:

- Start Values: Initializes the slider with a range from 1900 to 2024.

- Range: Sets the minimum value to 1800 and the maximum value to the current year.

- Step: Sets the step size to 1 year.

- Tooltips: Enables tooltips to show current slider values.

- Format: Rounds the slider values for display.

- Slider Update Event: Updates the displayed date range when the slider values change.

## Submit Button Event:

- Fetch API Request: Sends a POST request to the backend API with the selected date range.

- Response Handling: Processes the response:

- Success: Calls renderData to populate the table with the received data.

- Error: Logs and alerts if there's an error.

## Data Rendering Function:

- Clear Previous Data: Clears any previous data from the table.

- No Data Found: Displays a message if no companies are found within the range.

- Populate Table: Adds a new row for each company in the response data.

# Summary

- This API endpoint allows clients to send a POST request with a date range to filter companies based on their founding dates. 

- The request payload is validated, dates are parsed and converted, the data is filtered using the Stockfind model, and a formatted response is returned. 

- Uses merge sorting algorithm to filter dates in order

- Interactive interface for selecting a date range and displaying companies founded within that range

- Dynamically fetches and displays data from a backend API




