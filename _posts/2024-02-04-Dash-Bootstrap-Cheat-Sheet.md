---
title: Dash Bootstrap Cheat Sheet
date: 2024-02-04 07:00:00 -0000 # Note the offset of -0000 is optional
categories: [dash, bootstrap]
tags: [dash, bootstrap, reference]  # TAG names should always be in lowercase
---

# Dash Bootstrap Cheat Sheet

Dash Bootstrap combines the power of Dash and Bootstrap, allowing you to easily style your Dash apps with familiar Bootstrap classes. Here's a cheatsheet to get you started:

Concepts:

1. Grid System:

   * Divide your layout into rows and columns with dbc.Row and dbc.Col components.
   * Specify column widths using Bootstrap grid classes like col-md-6 (6 columns on medium screens).
   * Example:
```python
dbc.Row([
    dbc.Col("Column 1", width=4),
    dbc.Col("Column 2", width=8),
])
```

2. Utility Classes:

* Apply various styles using Bootstrap utility classes like text-center, mt-3 (margin top 3), border-primary.
* Example:
```python
dbc.Button("Click Me", className="btn btn-primary mt-3")
```

3. Colors:

* Use Bootstrap color classes like text-primary, bg-success, border-warning.
Example:
```python
dbc.Card(
    [dbc.CardBody("This card has a success background")],
    className="bg-success text-white",
)
```

4. Typography:

* Control font size, weight, and style with Bootstrap typography classes like h1, lead, text-muted.
* Example:
```python
dbc.Heading("This is a heading", className="h2 text-center")
```
5. Other Components:

* Style other Bootstrap components like buttons, cards, alerts, etc. using their respective classes.
Tips:

* Explore the official Bootstrap documentation for more styling options: [https://getbootstrap.com/docs/5.2/getting-started/introduction/](https://getbootstrap.com/docs/5.2/getting-started/introduction/ "styiling")
* Refer to the Dash Bootstrap Theme Explorer for examples: [https://dash-bootstrap-components.opensource.faculty.ai/docs/themes/explorer/](https://dash-bootstrap-components.opensource.faculty.ai/docs/themes/explorer/ "examples")
* Use online tools like the Dash Bootstrap Cheatsheet: [https://dashcheatsheet.pythonanywhere.com/](https://dashcheatsheet.pythonanywhere.com/ "tools") for interactive exploration.

Additional Resources:

Dash Bootstrap Components Documentation: [https://dash-bootstrap-components.opensource.faculty.ai/](https://dash-bootstrap-components.opensource.faculty.ai/ "documentation")
AnnMarieW's Dash Bootstrap Cheatsheet: [https://github.com/AnnMarieW/dash-bootstrap-cheatsheet](https://github.com/AnnMarieW/dash-bootstrap-cheatsheet "cheatsheet")
How to Style your Dash App with Bootstrap Cheat Sheet (YouTube): [https://www.youtube.com/watch?v=VTO6Njy10dY](https://www.youtube.com/watch?v=VTO6Njy10dY "video guide")
Remember, this is just a starting point. Experiment with different classes and explore the vast possibilities of Dash Bootstrap styling to create beautiful and user-friendly dashboards!
