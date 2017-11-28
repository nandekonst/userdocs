Client

File

src/api/core/client.ts

Index {#index}

Properties
Public tokenManager
Methods
Public init Public terminate
Constructor {#constructor}

constructor(fetch:Function)
**Parameters :**NameTypeOptionalDescriptionfetchFunction
Methods {#methods}

Publicinit
init(opts: IAuthOptions, ...modules: IModule[])
**Parameters :**NameTypeOptionalDescriptionoptsIAuthOptionsmodulesIModule[]Returns :Promise<>
Publicterminate
terminate()
Returns :Promise<>
Properties {#inputs}

PublictokenManager
tokenManager:TokenManager
Type :TokenManager
DataOperationsModule:

File

src/api/dataops/dataOperationsModule.ts

Implements

IModule

Index {#index}

Methods
Public dataset Public init Public terminate
Methods {#methods}

Publicdataset
dataset(dataset:string)
**Parameters : **NameTypeOptionalDescriptiondatasetstringReturns :Dataset
Publicinit
init(projectID:string, tokenManager: TokenManager, requestAdapter: IRequestAdapter)
**Parameters : **NameTypeOptionalDescriptionprojectIDstringtokenManagerTokenManagerrequestAdapterIRequestAdapterReturns :Promise<>
Publicterminate
terminate()
Returns :Promise<any>
