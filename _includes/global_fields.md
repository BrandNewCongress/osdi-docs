### Common Fields

A set of common fields that appear on all resources is included first, for reference.

| Name          | Required in Response	| Type      | Description
|-----------    |-----------|-----------|--------------
|identifiers	|strings[]	|A unique string array of identifiers in the format `[system name]:[id]`. See the general concepts document for more information about identifiers.
|created_date	|true	|datetime   |The date and time the resource was created on the local system
|modified_date	|true	|datetime	|The date and time the resource was last modified on the local system
|modified_by	|false	|Person	|The last editor of the resource
