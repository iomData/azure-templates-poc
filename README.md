# Azure Templates POC

Este repositorio contiene plantillas de ARM/Bicep para desplegar de forma modular:

- **Azure Functions**  
- **Cosmos DB**  
- **Data Factory (ADF)**  
- **Event Hubs**  
- **Service Bus**

## Estructura

Cada carpeta incluye un `template.bicep` (o `template.json`) con:

- Parámetros mínimos
- Ejemplo de despliegue con Azure CLI

## Despliegue

```bash
az deployment group create \
  --resource-group mi-rg \
  --template-file ./azure-functions/template.bicep \
  --parameters functionAppName=myFunctionApp location=eastus
