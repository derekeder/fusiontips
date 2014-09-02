# fusiontips

Forked from [Google Code](http://code.google.com/p/gmaps-utility-gis/source/browse/trunk/fusiontips/src/fusiontips.js) to enable usage with the Fusion Tables v1 API.

This library allows MapTip and fires mouseover/mouseout event for FusionTableLayers. It uses mouse cursor tracking and pause delay to trigger FusionTableQuery. It is not true mouseover event, but should suit most use cases.

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
