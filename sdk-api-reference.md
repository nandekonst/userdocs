# Classes:

## Client

### File

`src/api/core/client.ts`

### Index {#index}

| **Properties** |
| :--- |
| Public [tokenManager](#tokenManager) |
| **Methods** |
| Public [init](#init) Public [terminate](#terminate) |

### Constructor {#constructor}

| `constructor(fetch:`[`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)`)` |
| :--- |
| **Parameters :**NameTypeOptionalDescriptionfetch[`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) |

### Methods {#methods}

| **Publicinit** |
| :--- |
| `init(opts: IAuthOptions, ...modules: IModule[])` |
| **Parameters :**NameTypeOptionalDescriptionopts`IAuthOptions`modules`IModule[]`**Returns :**`Promise<>` |

| **Publicterminate** |
| :--- |
| `terminate()` |
| **Returns :**`Promise<>` |

### Properties {#inputs}

| **PublictokenManager** |
| :--- |
| `tokenManager:TokenManager` |
| Type :`TokenManager` |

## DataOperationsModule:

### File

`src/api/dataops/dataOperationsModule.ts`

### Implements

`IModule`

### Index {#index}

| **Methods** |
| :--- |
| Public [dataset](#dataset) Public [init](#init) Public [terminate](#terminate) |

### Methods {#methods}

| **Publicdataset** |
| :--- |
| `dataset(dataset:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`)` |
| **Parameters : **NameTypeOptionalDescriptiondataset[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)**Returns :**[`Dataset`](../classes/Dataset.html) |

| **Publicinit** |
| :--- |
| `init(projectID:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)`, tokenManager: TokenManager, requestAdapter: IRequestAdapter)` |
| **Parameters : **NameTypeOptionalDescriptionprojectID[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string)tokenManager`TokenManager`requestAdapter`IRequestAdapter`**Returns :**`Promise<>` |

| **Publicterminate** |
| :--- |
| `terminate()` |
| **Returns :**`Promise<any>` |

## 

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

| **`Publicselect`** |
| :--- |
| `select()` |
| **Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

| **Publicupdate** |
| :--- |
| `update(data:`[`object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/object)`)` |
| **Parameters :**NameTypeOptionalDescriptiondata[`object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/object)**Returns :**[`any`](https://www.typescriptlang.org/docs/handbook/basic-types.html) |

### `Properties` {#inputs}

| **`Publicname`** |
| :--- |
| `name:`[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |
| Type :[`string`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string) |



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



