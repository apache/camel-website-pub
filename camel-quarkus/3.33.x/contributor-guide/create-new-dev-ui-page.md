# Create a new Dev UI page

This guide outlines how to create new Quarkus Dev UI pages for Camel Quarkus extensions.

## Creating general Dev UI pages

To create general Quarkus Dev UI pages for any extension, follow the [extension developers guide](https://quarkus.io/guides/dev-ui#guide-for-extension-developers).

## Creating Dev UI pages for Camel consoles

Camel can expose various [consoles](../../../manual/camel-console.md) from which JSON responses can be harnessed in the Quarkus Dev UI to display useful data.

Creating new pages to interact with consoles is made simple by a reusable component that takes care of handling the data exchanges between the UI and the backend console service.

For example, if you wanted to add a page for the Camel console `foo`, you would do the following.

1.  Create a new `.js` file within the extension deployment module at `src/main/resources/dev-ui/qwc-camel-foo.js`.
    
2.  Extend the `QwcCamelCore` component and provide a `render()` function to return your HTML content
    
    For example, to create a simple table view:
    
    ```javascript
    import {html} from 'qwc-hot-reload-element';
    // NOTE: if your Dev UI page lives outside of camel-quarkus-core then use the following instead of ./qwc-camel-core.js:
    // import ../camel-quarkus-core/qwc-camel-core.js
    import {QwcCamelCore} from "./qwc-camel-core.js";
    import {columnBodyRenderer} from '@vaadin/grid/lit.js';
    import '@vaadin/grid';
    import '@vaadin/grid/vaadin-grid-sort-column.js';
    
    export class QwcCamelFoo extends QwcCamelCore { (1)
        constructor() {
            super('route', {}); (2)
        }
    
        render() {
            return html`
                (3)
                <vaadin-grid .items="${super.consoleData()}" class="consoleData" theme="no-border row-stripes">
                    (4)
                    <vaadin-grid-column
                            header="Column A"
                            ${columnBodyRenderer((item) => super.codeStyleRenderer(item.dataA), [])}
                            resizable>
                    </vaadin-grid-column>
                    <vaadin-grid-column
                            header="Column B"
                            ${columnBodyRenderer((item) => super.codeStyleRenderer(item.dataB), [])}
                            resizable>
                    </vaadin-grid-column>
                </vaadin-grid>
            `;
        }
    }
    (5)
    customElements.define('qwc-camel-foo', QwcCamelFoo);
    ```
    
    <table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Extending <code>QwcCamelCore</code> will automatically configure hot reloading of data and provides some useful data formatting helper methods.</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Call <code>super</code>, passing the id of the Camel console (see more information below) and an optional map of options that the console can use for data filtering and other functions.</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Render your UI. You can use Vaadin components or plain HTML. The console data can be obtained via <code>super.consoleData()</code>.</td></tr><tr><td><i class="conum" data-value="4"></i><b>4</b></td><td>When iterating over the console data you can access the returned JSON fields by referring to their name. E.g. if the console returns JSON <code>[{"dataA": "valueA", "dataB": "valueB"}]</code> you can refer to the data like <code>item.dataA</code> etc.</td></tr><tr><td><i class="conum" data-value="5"></i><b>5</b></td><td>You must register the component at the end of the file.</td></tr></tbody></table>
    
3.  Finally, you must create a `BuildStep` to add a UI link to the extension Dev UI card as described in the [guide](https://quarkus.io/guides/dev-ui#adding-pages-to-the-dev-ui).
    

### Finding the Camel console ID

To find all available console IDs.

```shell
curl -s localhost:8080/q/camel/dev-console | jq 'to_entries[].value.id'
```

Or you can [search](https://github.com/search?q=repo%3Aapache%2Fcamel+%22%40DevConsole%22+language%3AJava&type=code&l=Java) the Apache Camel core codebase and look for the `name` attribute value on the `@DevConsole` annotation.