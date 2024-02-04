---
title: Dash Callback Cheat Sheet
date: 2024-02-3 07:00:00 -0000 # Note the offset of -0000 is optional
categories: [dash, callbacks]
tags: [dash, callback, reference]  # TAG names should always be in lowercase
---

# Dash Callback Cheat Sheet

Key Concepts:

* Reactivity: Callbacks automatically trigger whenever an input value changes.
* Declarative definition: You clearly define relationships between inputs and outputs.
* Component IDs: Uniquely identify each component in your layout.
* Component properties: Specify which part of a component to update (e.g., value, figure).
* Input/Output combinations: Connect related inputs to update relevant outputs.
* State storage: Use State to persist data between callback executions (e.g., dropdown selections).
* Chained callbacks: Use output of one callback as input to another for complex interactions.

Key Points:

* Trigger: Callbacks are triggered by changes in Input component properties, not State.
* Structure: A callback must have at least one Input and one Output, but State is optional.
* Function Arguments: All Inputs and States must be represented as arguments within the callback function.
* Return Value: The callback function returns data to the specified Output component property.

Additional Considerations:

* Dataframe Modifications: Always create a copy of the dataframe before modifying it within a callback to avoid unintended side effects.
* Unique Outputs: Each Output component/property pair can only be set by a single callback.
* Conditional Updates:
    * To prevent output updates, raise a PreventUpdate exception.
    * To update only specific outputs, return Dash.no_update for those that should remain unchanged.

```python
@app.callback(
    Output("my-graph", "figure"),  # Output
    Input("dropdown", "value"),   # Input
    State("memory-store", "data"), # State (optional)
)
def update_graph(dropdown_value, stored_data):
    # Process input, update data, generate output
    df_copy = stored_data.copy()  # Make a copy of the dataframe
    df_copy = df_copy[df_copy["category"] == dropdown_value]
    figure = create_figure(df_copy)
    return figure
```

Tips:

* Use meaningful component IDs for better readability.
* Keep callback functions concise and focused on specific updates.
* Test your callbacks thoroughly with different input values.
* Refer to the official Dash documentation for advanced features and examples: https://dash.plotly.com/

Additional Resources:

* Cheatsheet: https://hellodash.pythonanywhere.com/cheatsheet
* Basic Callbacks Tutorial: https://dash.plotly.com/basic-callbacks
* The Dash Callback Explained: https://www.youtube.com/watch?v=mTsZL-VmRVE
* I hope this cheat sheet helps you remember the core concepts of Plotly Dash Callbacks!