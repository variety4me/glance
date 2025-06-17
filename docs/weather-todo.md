
### Weather
Display weather information for a specific location. The data is provided by https://open-meteo.com/.

Example:

```yaml
- type: weather
  units: metric
  hour-format: 12h
  location: London, United Kingdom
```

> [!NOTE]
>
> US cities which have common names can have their state specified as the second parameter as such:
>
> * Greenville, North Carolina, United States
> * Greenville, South Carolina, United States
> * Greenville, Mississippi, United States


Preview:

![](images/weather-widget-preview.png)

Each bar represents a 2 hour interval. The yellow background represents sunrise and sunset. The blue dots represent the times of the day where there is a high chance for precipitation. You can hover over the bars to view the exact temperature for that time.

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| location | string | yes |  |
| units | string | no | metric |
| hour-format | string | no | 12h |
| hide-location | boolean | no | false |
| show-area-name | boolean | no | false |

##### `location`
The name of the city and country to fetch weather information for. Attempting to launch the applcation with an invalid location will result in an error. You can use the [gecoding API page](https://open-meteo.com/en/docs/geocoding-api) to search for your specific location. Glance will use the first result from the list if there are multiple.

##### `units`
Whether to show the temperature in celsius or fahrenheit, possible values are `metric` or `imperial`.

#### `hour-format`
Whether to show the hours of the day in 12-hour format or 24-hour format. Possible values are `12h` and `24h`.

##### `hide-location`
Optionally don't display the location name on the widget.

##### `show-area-name`
Whether to display the state/administrative area in the location name. If set to `true` the location will be displayed as:

```
Greenville, North Carolina, United States
```

Otherwise, if set to `false` (which is the default) it'll be displayed as:

```
Greenville, United States
```

### Todo

A simple to-do list that allows you to add, edit and delete tasks. The tasks are stored in the browser's local storage.

Example:

```yaml
- type: to-do
```

Preview:

![](images/todo-widget-preview.png)

To reorder tasks, drag and drop them by grabbing the top side of the task:

![](images/reorder-todo-tasks-prevew.gif)

To delete a task, hover over it and click on the trash icon.

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| id | string | no | |

##### `id`

The ID of the todo list. If you want to have multiple todo lists, you must specify a different ID for each one. The ID is used to store the tasks in the browser's local storage. This means that if you have multiple todo lists with the same ID, they will share the same tasks.

#### Keyboard shortcuts
| Keys | Action | Condition |
| ---- | ------ | --------- |
| <kbd>Enter</kbd> | Add a task to the bottom of the list | When the "Add a task" field is focused |
| <kbd>Ctrl</kbd> + <kbd>Enter</kbd> | Add a task to the top of the list | When the "Add a task" field is focused |
| <kbd>Down Arrow</kbd> | Focus the last task that was added | When the "Add a task" field is focused |
| <kbd>Escape</kbd> | Focus the "Add a task" field | When a task is focused |

