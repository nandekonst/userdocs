## FieldFilter

### File

`src/api/dataops/filteringApi.ts`

### Implements

[`IFieldFilter`](../interfaces/IFieldFilter.html)

### Index {#index}

| **Methods** |
| :--- |
| Public[isBetween](#isBetween)Public[isDifferentFrom](#isDifferentFrom)Public[isEqualOrGreaterThan](#isEqualOrGreaterThan)Public[isEqualOrLessThan](#isEqualOrLessThan)Public[isEqualTo](#isEqualTo)Public[isGreaterThan](#isGreaterThan)Public[isInArray](#isInArray)Public[isLessThan](#isLessThan)Public[isLike](#isLike)Public[isNotInArray](#isNotInArray)Public[isNotNull](#isNotNull)Public[isNull](#isNull)Public[satisfiesRegexp](#satisfiesRegexp) |

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



