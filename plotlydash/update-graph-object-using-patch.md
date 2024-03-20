# Update graph object using `Patch()`

Dash >=2.9 allows for partial property updates using `Patch()`.

> With Partial Property Updates, you can update your callbacks to send over the new y-axis data on its own without the rest of the figure. As a result, it reduces the size of the network payload by 50% (1 array of x data instead of 2 arrays of x and y data), and there can be a noticeable performance improvement to charts or tables with >10K points.

```python
app.layout = html.Div([
      dcc.Dropdown(df.columns, id="column-selected"),
      dcc.Graph(id="my-graph", figure=px.scatter(df, x=df.index, y=df.columns[1]))
])
@app.callback(Output("my-graph", "figure"), Input("column-selected", "value"),
 prevent_initial_call=True)
def update(value):
    patch_figure = Patch()
    patch_figure["data"][0]["y"] = df[value]
    return patch_figure
```


https://community.plotly.com/t/dash-2-9-2-released-partial-property-updates-with-patch-duplicate-outputs-dcc-geolocation-scatter-group-attributes-and-more/72114

https://dash.plotly.com/partial-properties?_gl=1*1g7oip3*_ga*MTAzOTkyOTIzOS4xNjk5NTM2NTE0*_ga_6G7EE0JNSC*MTcxMDk0MzMwMi4yMC4xLjE3MTA5NDY4ODMuNTUuMC4w