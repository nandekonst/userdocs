
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

| `Publicexecute` |
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
