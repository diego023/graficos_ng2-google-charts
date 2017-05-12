# ng2-google-charts

> Google Charts module for Angular 2

Please see [this page][example-page] for a live demo.

[![NPM Version][npm-image]][npm-url]
[![Downloads][npm-downloads-image]][npm-downloads-url]

## Install

```bash
npm i --save ng2-google-charts
```

## Usage

Import the `Ng2GoogleChartsModule` in your `app.module.ts`:
```ts
import { Ng2GoogleChartsModule } from 'ng2-google-charts';

@NgModule({
  ...
  imports: [
    ...
    Ng2GoogleChartsModule,
  ],
})
export class AppModule { }
```

In your templates, use the `google-chart` component like this:
```html
<google-chart [data]="pieChartOptions"></google-chart>
```
and in the corresponding `.ts` file:
```ts
pieChartOptions =  {
  chartType: 'PieChart',
  dataTable: [
    ['Task', 'Hours per Day'],
    ['Work',     11],
    ['Eat',      2],
    ['Commute',  2],
    ['Watch TV', 2],
    ['Sleep',    7]
  ],
  options: {'title': 'Tasks'},
};
```

## Formatters

You can specify an array of multiple formatter types and configurations like
this:
```ts
public tableChartOptions =  {
  chartType: 'Table',
  dataTable: [
    ['Department', 'Revenues', 'Another column'],
    ['Shoes', 10700, -100],
    ['Sports', -15400, 25],
    ['Toys', 12500, 40],
    ['Electronics', -2100, 889],
    ['Food', 22600, 78],
    ['Art', 1100, 42]
  ],
  formatters: [
    {
      columns: [1, 2],
      type: 'NumberFormat',
      options: {
        prefix: '&euro;', negativeColor: '#FF0000', negativeParens: true
      }
    }
  ],
  options: {title: 'Countries', allowHtml: true}
};
```

Please refer to the Google Chart [documentation for formatter types and options](https://developers.google.com/chart/interactive/docs/reference#formatters).

Please see [this page][example-page] for a demo with more examples.

## Events

### chartReady

The `chartReady` event is fired when a chart is completely loaded.

Bind the `chartReady` event in the `google-chart` component like this:
```html
<google-chart [data]='pieChartOptions' (chartReady)='ready($event)'></google-chart>
```

Your `ready()` function is passed an event whose interface looks like this:
```ts
interface ChartReadyEvent {
  message: string;
}
```

You can import the `ChartReadyEvent` interface in your `.ts` file:
```ts
import { ChartReadyEvent } from 'ng2-google-charts';
```

and then use it like:
```ts
public ready(event: ChartReadyEvent) {
  // your logic
}
```

### chartError

The `chartError` event is fired if there are some errors with a chart.

Bind the `chartError` event in the `google-chart` component, like this:
```html
<google-chart [data]='pieChartOptions' (chartError)='error($event)'></google-chart>
```

Your `error()` function is passed an event whose interface looks like this:
```ts
interface ChartErrorEvent {
  id: string;
  message: string;
  detailedMessage: string;
  options: Object;
}
```

You can import the `ChartErrorEvent` interface in your `.ts` file:
```ts
import { ChartErrorEvent } from 'ng2-google-charts';
```

and then use it like:
```ts
public error(event: ChartErrorEvent) {
  // your logic
}
```

See more details about [returned values for error event][google-charts-error-event].

### chartSelect

The `chartSelect` event is fired when a chart is selected/clicked.

Bind the `chartSelect` event in the `google-chart` component, like this:
```html
<google-chart [data]='pieChartOptions' (chartSelect)='select($event)'></google-chart>
```

Your `select()` function is passed an event whose interface looks like this:
```ts
interface ChartSelectEvent {
  message: string;
  row: number | null;
  column: number | null;
  selectedRowValues: any[];
}
```

You can import the `ChartSelectEvent` interface in your `.ts` file:
```ts
import { ChartSelectEvent } from 'ng2-google-charts';
```

and then use it like:
```ts
public select(event: ChartSelectEvent) {
  // your logic
}
```

### mouseOver

The `mouseOver` event is fired when the user moves the mouse over some chart
item.

Bind the `MouseOver` event in the `google-chart` component like this:
```html
<google-chart [data]="comboChartOptions" (mouseOver)="mouseOver($event)"></google-chart>
```

Your `mouseOver()` function is passed an event whose interface looks like this:
```ts
interface MouseOverEvent {
  position: DataPointPosition;
  boundingBox: BoundingBox;
  value: any;
  tooltip: ChartHTMLTooltip | null;
  columnType: string;
  columnLabel: string;
}
```

You can import the `MouseOverEvent` interface in your `.ts` file:
```ts
import { MouseOverEvent } from 'ng2-google-charts';
```

and then use it like:
```ts
public mouseOver(event: MouseOverEvent) {
  // your logic
}
```

## License

[MIT](LICENSE.md)

[npm-image]: https://img.shields.io/npm/v/ng2-google-charts.svg
[npm-url]: https://npmjs.org/package/ng2-google-charts
[npm-downloads-image]: http://img.shields.io/npm/dm/ng2-google-charts.svg
[npm-downloads-url]: https://npmjs.org/package/ng2-google-charts
[example-page]: https://gmazzamuto.github.io/ng2-google-charts
[google-charts-error-event]: https://developers.google.com/chart/interactive/docs/events#the-error-event
