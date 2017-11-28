
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

| **Public tokenManager** |
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
