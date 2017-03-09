# Querying Lifecycle Stages


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/lifecycleStage/version/3/do/query?...` | `user_key, api_key` | Returns the lifecycle stage matching the specified criteria parameters. See the [Using Lifecycle Stages](#using-lifecycle-stages) section for a complete description of the lifecycle stage [XML Response Format](#xml-response-format). Also see [Lifecycle Stage](object-field-references#lifecycle-stage) in [Object Field References](object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 lifecycle stages will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for lifecycle stages with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for lifecycle stages with IDs less than the specified integer |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the lifecycle stages matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching lifecycle stage (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching lifecycle stage will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th lifecycle stage matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in lifecycle stage queries, see Lifecycle Stage in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `position` | `ascending` | Specifies that the query results should be sorted by the Lifecycle Stages' `position` fields |
| `id` | `ascending` | Specifies that the query results should be sorted by the Lifecycle Stages' `id` fields |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <lifecycleStage>...</lifecycleStage>
        <lifecycleStage>...</lifecycleStage>
        <lifecycleStage>...</lifecycleStage>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting lifecycle stages for the specified query |
| `<total_results>` | Contains the number of lifecycle stages selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched lifecycle stages |
| `<lifecycleStage>` | The data for an individual lifecycle stage. See [Using Lifecycle Stages](#using-lifecycle-stages) for a complete description of the lifecycle stage [XML Response Format](#xml-response-format). Also see [Lifecycle Stage](object-field-references#lifecycle-stage) in [Object Field References](object-field-references) |


# Using Lifecycle Stages

## XML Response Format

```
<rsp stat="ok" version="1.0">
    <lifecycleStage>
        <id>912</id>
        <name>Prospects</name>
        <position>0</position>
        <is_locked>true</is_locked>
    </lifecycleStage>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<lifecycleStage>` | Parent tag. Contains data fields for target lifecycle stage. For complete field listing, see [Lifecycle Stage](object-field-references#lifecycle-stage) in [Object Field References](object-field-references). |
