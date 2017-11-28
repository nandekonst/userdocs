# Classes:


## DataRequest:

### File

`src/api/dataops/dataRequest.ts`

### Index {#index}

| **Properties** |
| :--- |
| Public [Action](#Action) Public [Records](#Records) |
| **Methods** |
| Public [execute](#execute) |

### Constructor {#constructor}

| `constructor(action:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, dataset:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionaction[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)dataset[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

### Methods {#methods}

| **Publicexecute** |
| :--- |
| `execute(queryExecuter: RequestExecuter)` |
| **Parameters :**NameTypeOptionalDescriptionqueryExecuter`RequestExecuter`**Returns :**`Promise<any>` |

### Properties {#inputs}

| **PublicAction** |
| :--- |
| `Action:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |
| Type :[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

| **PublicRecords** |
| :--- |
| `Records:Array<object>` |
| Type :`Array<object>` |

## Dataset:

### File

`src/api/dataops/dataset.ts`

### Implements

[`IResource`](../interfaces/IResource.html)

### Index {#index}

| **Properties** |
| :--- |
| Public [name](#name) |
| **Methods** |
| Public [delete](#delete) Public [insert](#insert) Public [select](#select) Public [update](#update) |

### Constructor {#constructor}

| `constructor(dataset:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, queryExecuterBuilder: QueryExecuterBuilder)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptiondataset[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)queryExecuterBuilder`QueryExecuterBuilder` |

### Methods {#methods}

| **Publicdelete** |
| :--- |
| `delete()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicinsert** |
| :--- |
| `insert(records: Array)` |
| **Parameters :**NameTypeOptionalDescriptionrecords`Array<object>`**Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| `Publicselect` |
| :--- |
| `select()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicupdate** |
| :--- |
| `update(data:`[`object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/object)`)` |
| **Parameters :**NameTypeOptionalDescriptiondata[`object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/object)**Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

### `Properties` {#inputs}

| `Publicname` |
| :--- |
| `name:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |
| Type :[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

## 

## DeleteQuery:

### File

`src/api/dataops/deleteQuery.ts`

### Implements

[`IFields`](../interfaces/IFields.html)[`ILimit`](../interfaces/ILimit.html)[`IOffset`](../interfaces/IOffset.html)[`IFilterable`](../interfaces/IFilterable.html)[`IExecutable`](../interfaces/IExecutable.html)[`ISortable`](../interfaces/ISortable.html)

### Index {#index}

| **Methods** |
| :--- |
| Public [execute](#execute) Public [fields](#fields) Public [limit](#limit) Public [offset](#offset) Public [sortAsc](#sortAsc) Public [sortDesc](#sortDesc) Public [where](#where) |

### Constructor {#constructor}

| `constructor(queryExecuter: RequestExecuter, dataset:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionqueryExecuter`RequestExecuter`dataset[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

### Methods {#methods}

| **Publicexecute** |
| :--- |
| `execute()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicfields** |
| :--- |
| `fields(...fields: string[])` |
| **Parameters :**NameTypeOptionalDescriptionfields`string[]`**Returns :**[`DeleteQuery`](../classes/DeleteQuery.html) |

| **Publiclimit** |
| :--- |
| `limit(limit:`[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)`)` |
| **Parameters :**NameTypeOptionalDescriptionlimit[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)**Returns :**[`DeleteQuery`](../classes/DeleteQuery.html) |

| **Publicoffset** |
| :--- |
| `offset(offset:`[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)`)` |
| **Parameters :**NameTypeOptionalDescriptionoffset[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)**Returns :**[`DeleteQuery`](../classes/DeleteQuery.html) |

| **PublicsortAsc** |
| :--- |
| `sortAsc(...fields: string[])` |
| **Parameters :**NameTypeOptionalDescriptionfields`string[]`**Returns :**[`DeleteQuery`](../classes/DeleteQuery.html) |

| **PublicsortDesc** |
| :--- |
| `sortDesc(...fields: string[])` |
| **Parameters :**NameTypeOptionalDescriptionfields`string[]`**Returns :**[`DeleteQuery`](../classes/DeleteQuery.html) |

| **Publicwhere** |
| :--- |
| `where(filter:`[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html)`)` |
| **Parameters :**NameTypeOptionalDescriptionfilter[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html)**Returns :**[`DeleteQuery`](../classes/DeleteQuery.html) |



## FieldFilter:

### File

`src/api/dataops/filteringApi.ts`

### Implements

[`IFieldFilter`](../interfaces/IFieldFilter.html)

### Index {#index}

| **Methods** |
| :--- |
| Public [isBetween](#isBetween) Public [isDifferentFrom](#isDifferentFrom) Public [isEqualOrGreaterThan](#isEqualOrGreaterThan) Public [isEqualOrLessThan](#isEqualOrLessThan) Public [isEqualTo](#isEqualTo) Public [isGreaterThan](#isGreaterThan) Public [isInArray](#isInArray) Public [isLessThan](#isLessThan) Public [isLike](#isLike) Public [isNotInArray](#isNotInArray) Public [isNotNull](#isNotNull) Public [isNull](#isNull) Public [satisfiesRegexp](#satisfiesRegexp) |

### Constructor {#constructor}

| `constructor(fieldName:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionfieldName[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

### Methods {#methods}

| **PublicisBetween** |
| :--- |
| `isBetween(start:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, end:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionstart[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)end[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisDifferentFrom** |
| :--- |
| `isDifferentFrom(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisEqualOrGreaterThan** |
| :--- |
| `isEqualOrGreaterThan(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisEqualOrLessThan** |
| :--- |
| `isEqualOrLessThan(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisEqualTo** |
| :--- |
| `isEqualTo(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisGreaterThan** |
| :--- |
| `isGreaterThan(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisInArray** |
| :--- |
| `isInArray(values: string[])` |
| **Parameters :**NameTypeOptionalDescriptionvalues`string[]`**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisLessThan** |
| :--- |
| `isLessThan(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisLike** |
| :--- |
| `isLike(value:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionvalue[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisNotInArray** |
| :--- |
| `isNotInArray(values: string[])` |
| **Parameters :**NameTypeOptionalDescriptionvalues`string[]`**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisNotNull** |
| :--- |
| `isNotNull()` |
| **Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicisNull** |
| :--- |
| `isNull()` |
| **Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |

| **PublicsatisfiesRegexp** |
| :--- |
| `satisfiesRegexp(regexp:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters :**NameTypeOptionalDescriptionregexp[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html) |



## FilteringCriterion:

### File

`src/api/dataops/filteringApi.ts`

### Implements

[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html)

### Index {#index}

| **Methods** |
| :--- |
| Public [and](#and) Public [or](#or) |

### Constructor {#constructor}

| `constructor(lowLevelCondition?: ICondition, highLevelCriteria?:`[`FilteringCriterion`](../classes/FilteringCriterion.html)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionlowLevelCondition`ICondition`truehighLevelCriteria[`FilteringCriterion`](../classes/FilteringCriterion.html)true |

### Methods {#methods}

| **Publicand** |
| :--- |
| `and(conditionToAdd:`[`FilteringCriterion`](../classes/FilteringCriterion.html)`)` |
| **Parameters :**NameTypeOptionalDescriptionconditionToAdd[`FilteringCriterion`](../classes/FilteringCriterion.html)**Returns :**[`FilteringCriterion`](../classes/FilteringCriterion.html) |

| **Publicor** |
| :--- |
| `or(conditionToAdd:`[`FilteringCriterion`](../classes/FilteringCriterion.html)`)` |
| **Parameters :**NameTypeOptionalDescriptionconditionToAdd[`FilteringCriterion`](../classes/FilteringCriterion.html)**Returns :**[`FilteringCriterion`](../classes/FilteringCriterion.html) |

## 

## InsertQuery:

### File

`src/api/dataops/insertQuery.ts`

### Implements

[`IExecutable`](../interfaces/IExecutable.html)

### Index {#index}

| **Methods** |
| :--- |
| Public [execute](#execute) |

### Constructor {#constructor}

| `constructor(queryExecuter: RequestExecuter, records: Array, dataset:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionqueryExecuter`RequestExecuter`records`Array<object>`dataset[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

### `Methods` {#methods}

| **`Publicexecute`** |
| :--- |
| `execute()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |



## RTCModule:

### File

`src/api/realtime/rtcModule.ts`

### Implements

`IModule`

### Index {#index}

| **Methods** |
| :--- |
| Public [init](#init) Public [pendingSubscriptionRequests](#pendingSubscriptionRequests) Public [subscribe](#subscribe) Public [terminate](#terminate) Public [unsubscribe](#unsubscribe) |

### Constructor {#constructor}

| `constructor(messageReceivedCallback:`[`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)`, websocketCreateCallback?:`[`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionmessageReceivedCallback[`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)websocketCreateCallback[`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)true |

### Methods {#methods}

| **Publicinit** |
| :--- |
| `init(projectID:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, tokenManager: TokenManager, requestAdapter: IRequestAdapter)` |
| **Parameters :**NameTypeOptionalDescriptionprojectID[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)tokenManager`TokenManager`requestAdapter`IRequestAdapter`**Returns :**`Promise<>` |

| **PublicpendingSubscriptionRequests** |
| :--- |
| `pendingSubscriptionRequests()` |
| **Returns :**`string[]` |

| **Publicsubscribe** |
| :--- |
| `subscribe(method:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, resource:`[`IResource`](../interfaces/IResource.html)`)` |
| **Parameters :**NameTypeOptionalDescriptionmethod[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)resource[`IResource`](../interfaces/IResource.html)**Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicterminate** |
| :--- |
| `terminate()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicunsubscribe** |
| :--- |
| `unsubscribe(method:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, resource:`[`IResource`](../interfaces/IResource.html)`)` |
| **Parameters :**NameTypeOptionalDescriptionmethod[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)resource[`IResource`](../interfaces/IResource.html)**Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |



## SelectQuery:

### File

`src/api/dataops/selectQuery.ts`

### Implements

[`IFields`](../interfaces/IFields.html)[`ILimit`](../interfaces/ILimit.html)[`IOffset`](../interfaces/IOffset.html)[`IFilterable`](../interfaces/IFilterable.html)[`IExecutable`](../interfaces/IExecutable.html)[`IRelational`](../interfaces/IRelational.html)[`ISortable`](../interfaces/ISortable.html)

### Index {#index}

| **Methods** |
| :--- |
| Public [execute](#execute) Public [fields](#fields) Public [limit](#limit) Public [offset](#offset) Public [relation](#relation) Public [sortAsc](#sortAsc) Public [sortDesc](#sortDesc) Public [where](#where) |

### Constructor {#constructor}

| `constructor(queryExecuter: RequestExecuter, dataset:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionqueryExecuter`RequestExecuter`dataset[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |

### Methods {#methods}

| **Publicexecute** |
| :--- |
| `execute()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicfields** |
| :--- |
| `fields(...fields: string[])` |
| **Parameters :**NameTypeOptionalDescriptionfields`string[]`**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |

| **Publiclimit** |
| :--- |
| `limit(limit:`[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)`)` |
| **Parameters :**NameTypeOptionalDescriptionlimit[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |

| **Publicoffset** |
| :--- |
| `offset(offset:`[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)`)` |
| **Parameters :**NameTypeOptionalDescriptionoffset[`number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/number)**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |

| **Publicrelation** |
| :--- |
| `relation(dataSet:`[`Dataset`](../classes/Dataset.html)`, callback: (query:`[`SelectQuery`](../classes/SelectQuery.html)`) => void)` |
| **Parameters :**NameTypeOptionalDescriptiondataSet[`Dataset`](../classes/Dataset.html)callback[`function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/function)**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |

| **PublicsortAsc** |
| :--- |
| `sortAsc(...fields: string[])` |
| **Parameters :**NameTypeOptionalDescriptionfields`string[]`**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |

| **PublicsortDesc** |
| :--- |
| `sortDesc(...fields: string[])` |
| **Parameters :**NameTypeOptionalDescriptionfields`string[]`**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |

| **Publicwhere** |
| :--- |
| `where(filter:`[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html)`)` |
| **Parameters :**NameTypeOptionalDescriptionfilter[`IFilteringCriterion`](../interfaces/IFilteringCriterion.html)**Returns :**[`SelectQuery`](../classes/SelectQuery.html) |



