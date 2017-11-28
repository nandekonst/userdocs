



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



