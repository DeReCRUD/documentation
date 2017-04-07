# Model

### <a name="struct"></a> Struct

This is the primary object...

| Field   | Type                      | Required | Notes                                                  |
|---------|---------------------------|----------|--------------------------------------------------------|
| name    | ref                       | true     | The common name used to identity the type of structure |
| label   | string or [Label](#label) | true     | Describes the struct in the UI                         |
| collectionLabel | string or [Label](#label) | true | Describes a collection of the struct in the UI     |
| fields  | [Field](#field)[]         | true     |                                                        |
| blocks  | [block](#block)[]         | true     | Array of [blocks](#block)


### <a name="field></a> Field

The property level portions of a [struct](#struct)

| Field   | Type          | Required | Missing Val | Notes                                     |
|---------|---------------|----------|------------ |-------------------------------------------|
| name    | ref           | true     | N/A         | The common name used to describe identify the field |
| label   | string or [Label](#label)| true | N/A  | Describes the field in the UI             |
| type    | string        | true     | N/A         | Identifies the [Type](#type) of the field |
| key_field | boolean     | false    | false       | Indicates that the field is used as the key or part of a composite key to identify a specific instance of a struct |
| required| boolean       | false    | false       | Indicates that the field is required in order to be saved |
| unique  | boolean       | false    | false       | The field value must be unique across all instances of the same struct |
| initial_value | value cosistent with the field [type](#type) | false |  | The value used when an instance of the struct is created |
| missing_value | value cosistent with the field [type](#type) | false |  | The value to be used if a value for the struct has not been set |
| placeholder | string    | false    |             | A string to display in the UI when no value is defined |
| hints       | [hint](#hint) | false |            | Display recomendation to the UI   |


#### Additional properties for fields of [type](#type) text

| Field   | Type          | Required | Missing Val | Notes                                     |
|---------|---------------|----------|------------ |-------------------------------------------|
| maxlength | integer     | false    |             | The longest allowed length of the value   |
| minlength | integer     | false    |             | The shortest allowed length of the value  | 


#### Additional properties for fields of [type](#type) integer

| Field   | Type          | Required | Missing Val | Notes                                     |
|---------|---------------|----------|------------ |-------------------------------------------|
| max     | integer       | false    |             | The maxiumum allowed value                |
| min     | integer       | false    |             | The minimum allowed value                 | 


#### Additional properties for fields of [type](#type) list

| Field   | Type          | Required | Missing Val | Notes                                     |
|---------|---------------|----------|------------ |-------------------------------------------|
| options | [option](#option)[] | true | N/A       | An array of values [options](#option)     | 


#### Additional properties for fields of [type](#type) foreignKey

| Field     | Type                     | Required | Missing Val | Notes                                     |
|-----------|--------------------------|----------|------------ |-------------------------------------------|
| reference | [reference](#reference)  | true     | N/A         | A [reference](#reference) to the child struct |


#### Additional properties for fields of [type](#type) linkedStruct

| Field     | Type                     | Required | Missing Val | Notes                                     |
|-----------|--------------------------|----------|------------ |-------------------------------------------|
| reference | [reference](#reference)  | true     | N/A         | A [reference](#reference) to the other struct |


#### Additional properties for fields of [type](#type) derived

| Field     | Type      | Required | Missing Val | Notes                                         |
|-----------|-----------|----------|------------ |-----------------------------------------------|
| pattern   | text      | true     | N/A         | A pattern describing how a value is derived from other fields |


### <a name="type"></a> Type


| Type         | Description                                       |
|--------------|---------------------------------------------------|
| text         |                                                   |
| ref          | A string with no whitespace characters            |
| integer      |                                                   |
| estimate     | The approximation of an decimal value             |
| date         |                                                   |
| boolean      |                                                   |
| percent      |                                                   |
| money        |                                                   |
| foreignKey   | Indicates a parent relationship of another struct |
| linkedStruct | Indicates a relationship to another struct        |
| list         | A preset list of possible values                  |
| derived      | A value derived from the values of other fields   |


### <a name="block"></a> Block

A grouping of fields displayed in the UI

| Field   | Type          | Required  | Notes                                          |
|---------|---------------|-----------|------------------------------------------------|
| name    | ref           | true      | The common name used to identify the block     |
| label   | string or [Label](#label) | false | Describes the block in the UI          |
| fields  | string[]      | true      | Array of fieldnames included in the block      |
| hints   | [hint](#hint) | false     | Display recomendation to the UI                |


### <a name="label"></a> Label

Describes how to label a struct, field, or block.  The object must contain as least
one of the following.

| Field   | Data Type | Required | Notes                            |
|---------|-----------|----------|----------------------------------|
| short   | string    | false    | The short length label           |
| medium  | string    | false    | The medium length label          |
| long    | string    | false    | The long length label            |


### <a name="reference"></a> Reference

Describes a relationship to another struct

| Field       | Type     | Required | Missing Val | Notes                                     |
|-------------|----------|----------|------------ |-------------------------------------------|
| name        | ref      | true     | N/A         | The name of the other [struct](#struct)   |
| label_field | string   | true     | N/A         | The name of the [field](#field) whose value will identify the other [struct](#struct) instance.


### <a name="hint"></a> Hint

Recommendations given to the UI about how to display the form element.  Applies to [fields](#field) and [structs](#struct)

| Field       | Type     | Required | Missing Val | Notes                                       |
|-------------|----------|----------|------------ |---------------------------------------------|
| width       | integer  | false    |             | The recommended width of a field or block   |


### <a name="option"></a> Option


| Field    | Type                     | Required | Notes                                       |
|----------|--------------------------|----------|---------------------------------------------|
| label    | string or [Label](#label)| true     | The display value for the option in the UI  |
| value    | value cosistent with the field [type](#type) | true | the value associated with the option |
