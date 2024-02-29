### Tareas para crear un contenedor 
por defecto el contendor es $web y el cual permite acceder a su contenido con la URL del storage. Por tal motivo
se retiro las siguientes tareas del .yml que crea el Storage

- task: AzureCLI@2
  displayName: 'Habilitar acceso anónimo en la cuenta de almacenamiento'
  inputs:
    azureSubscription: 'AzureResourceManager'
    scriptType: 'ps'
    scriptLocation: 'inlineScript'
    inlineScript: |
      az storage account update --name appiumtestreport --resource-group GR-QA --allow-blob-public-access true

- task: AzureCLI@2
  displayName: 'Crear contenedor en la cuenta de almacenamiento'
  inputs:
    azureSubscription: 'AzureResourceManager'
    scriptType: 'ps'
    scriptLocation: 'inlineScript'
    inlineScript: |
      az storage container create --name '$web' --account-name appiumtestreport --account-key $(StorageAccountKey) --public-access blob