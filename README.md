# fusiontips

Forked from [Google Code](http://code.google.com/p/gmaps-utility-gis/source/browse/trunk/fusiontips/src/fusiontips.js) to enable usage with the Fusion Tables v1 API.

This library allows MapTip and fires mouseover/mouseout event for FusionTableLayers. It uses mouse cursor tracking and pause delay to trigger FusionTableQuery. It is not true mouseover event, but should suit most use cases.

## Usage

### Include Scripts
This library enables map tips and mouseover/mouseout for FusionTablesLayer
The first step is to include `fusiontips.js` in your document header, after GMaps API is load. You can use the online version if you do not want to download the script.

```html
<script src="/path/to/fusiontips.js" type="text/javascript"></script>
```

### Enable Map tips
You can simply call google.maps.FusionTablesLayer.enableMapTips(options) to enable it.

```javascript
function init(){
  var tableid = 297050;
  var googleApiKey = "xxxxxx"; //get yours at https://code.google.com/apis/console/
  layer = new google.maps.FusionTablesLayer({
    query: {
      select: 'Address',
      from: tableid
    },
    map: map
  });
  layer.enableMapTips({
    select: "'Store Name','Address'", // list of columns to query, typially need only one column.
    from: tableid, // fusion table name
    geometryColumn: 'Address', // geometry column name
    suppressMapTips: false, // optional, whether to show map tips. default false
    delay: 200, // milliseconds mouse pause before send a server query. default 300.
    tolerance: 8, // tolerance in pixel around mouse. default is 6.
    googleApiKey: googleApiKey,
    tipHtmlRowsTemplateFunction: function(rows) {
        return 'Details: <b>My Column1: </b>' + rows[0][0] + '<br><b>My Column2: </b>'+rows[0][1];
      } 
  });
  //listen to events if desired.
  google.maps.event.addListener(layer, 'mouseover', function(fEvent) {
    var row = fEvent.row;
    myHtml = 'mouseover:<br/>';
    for (var x in row) {
      if (row.hasOwnProperty(x)) {
        myHtml += '<b>' + x + "</b>:" + row[x].value + "<br/>";
      }
    }
    document.getElementById('info').innerHTML = myHtml;
  });
  google.maps.event.addListener(layer, 'mouseout', function(fevt) {
    document.getElementById('info').innerHTML = '';
  });
}
```

## Examples

* [Point, Line and Polygon](http://derekeder.github.io/fusiontips/examples/point-line-polygon/fusiontips.html)
* [Hover and search - points](http://derekeder.github.io/fusiontips/examples/search-and-hover/points-hover-add-search.html)
* [Hover and search - polygon](http://derekeder.github.io/fusiontips/examples/search-and-hover/polygon-hover-add-search.html)

## Reference

### <a name="google.maps.FusionTablesLayer"></a>class FusionTablesLayer

These are new methods added to the Google Maps API's
[FusionTablesLayer](http://code.google.com/apis/maps/documentation/javascript/reference.html#FusionTablesLayer)
class.

#### Methods
<table summary="class FusionTablesLayer - Methods" >

  <tbody>
    <tr>
      <th>Methods</th>

          <th>Return&nbsp;Value</th>

      <th>Description</th>
    </tr>

      <tr class="odd">
        <td>disableMapTips()</td>

            <td>None</td>

        <td>Disable map tips for the fusion layer.</td>
      </tr>

      <tr class="even">
        <td>enableMapTips(<span class="type">opts:MapTipOptions</span>)</td>

            <td>None</td>

        <td>Enable map tips for the fusion layer. The user can hover over a fusion feature, pause for a small time, then get a map tip.</td>
      </tr>

  </tbody>
</table>

#### Events

<table summary="class FusionTablesLayer - Events" >
  <tbody>
    <tr>
      <th>Events</th>

          <th>Arguments</th>

      <th>Description</th>
    </tr>

      <tr class="odd">
        <td>mouseout</td>

            <td>None</td>

        <td>This event is fired when the mouse out of a fusion feature.</td>
      </tr>

      <tr class="even">
        <td>mouseover</td>

            <td><span class="type">mouseevent:FusionTablesMouseEvent</span></td>

        <td>This event is fired when the mouse over a fusion feature. Contains: infoWindowHtml, latLng, row.</td>
      </tr>

  </tbody>
</table>

### <a name="MapTipOptions"></a>class MapTipOptions

This class represents the optional parameter passed into google.maps.FusionTablesLayer.enableMapTips.  There is no constructor for this class.  Instead, this class is instantiated as a javascript object literal.

#### Properties
<table summary="class MapTipOptions - Properties" >

  <tbody>
    <tr>
      <th>Properties</th>

          <th>Type</th>

      <th>Description</th>
    </tr>

      <tr class="even">
        <td>googleApiKey</td>

            <td>string</td>

        <td>required. api key for accessing the Fusion Tables v1 API. [Get one here](https://code.google.com/apis/console/).</td>
      </tr>

      <tr class="odd">
        <td>delay</td>

            <td>number</td>

        <td>optional. milliseconds mouse pause before send a server query. default 500.</td>
      </tr>

      <tr class="even">
        <td>from</td>

            <td>String</td>

        <td>required. fusion table id.</td>
      </tr>

      <tr class="odd">
        <td>geometryColumn</td>

            <td>String</td>

        <td>required. fusion table's geometry column name.</td>
      </tr>

      <tr class="even">
        <td>select</td>

            <td>String</td>

        <td>required. list of columns (by comma) to query, typically need only one column. e.g "'Store Name','Address'"</td>
      </tr>

      <tr class="odd">
        <td>style</td>

            <td>Object</td>

        <td>optional. the css style of map tip.</td>
      </tr>

      <tr class="even">
        <td>suppressMapTips</td>

            <td>bool</td>

        <td>optional, whether to show map tips. default false</td>
      </tr>

      <tr class="odd">
        <td>tolerance</td>

            <td>number</td>

        <td>required. tolerance in pixel around mouse. default is 6.</td>
      </tr>

      <tr class="even">
        <td>where</td>

            <td>String</td>

        <td>optional. "where" filter for select.</td>
      </tr>

  </tbody>
</table>

## Contributors 

* [Nianwei Liu](http://code.google.com/u/104139885275196935151/) - original library owner
* [Gary Little](http://code.google.com/u/117613638752768553824/) - contributor to original library
* [Derek Eder](https://github.com/derekeder) - Fusion Tables v1 API updates
* [Chad Skelton](https://github.com/chadskelton) - search and hover examples

## Note on Patches/Pull Requests
 
* Fork the project.
* Make your feature addition or bug fix.
* Commit and send me a pull request.

## License

Released under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)
