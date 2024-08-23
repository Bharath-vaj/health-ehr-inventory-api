
# Mule Healthcare Application Project

## Overview

This project contains a Mule application designed to integrate and process healthcare data. The application includes several APIs and libraries to handle different aspects of the healthcare domain.

## Project Structure

The project is organized into the following main components:

### 1.Health Common Library

The `health-common-library` module contains reusable library across different APIs RAML.

`health-common-library` contents:

- `securitySchemes` : Contains the `clientIdEnforcement` security schema, designed for reuse in all APIs. This schema authenticates using the `client_id` and `client_secret` generated in the Anypoint platform.
- `types` : Types includes all the common data type use across all system APIs.
- `traits` : Traits include the common error response used for all the request defined in each API. 

This library aims to centralize and standardize key elements, promoting consistency and efficiency in API development.

### 2.Health Common DataWeave Library

The `health-common-dw-library` module contains reusable DataWeave functions and scripts used across different APIs.

`health-common-dw-library` contents under src/main/dw:

- `HL7parsefunctions.dwl` : This file contains reusable functions for converting HL7 file contents into a JSON readable format.
- `HL7segmentfunctions.dwl` : This file contains reusable functions for converting JSON formatted data into HL7 segments format.

These resources are designed to enhance efficiency and maintainability by providing standardized functions for common data transformation tasks in DataWeave.

### 2. Drex SAPI

The `health-drex-sapi` module is a Mule application for processing healthcare data related to Drex end system.

This system API facilitates the retrieval of `Patient blood test` data from the Drex end system.

### 3. Chirp SAPI

The `health-chirp-sapi` module is a Mule application for processing healthcare data related to Chirp end system.

This system API facilitates the retrieval of `Patient immunization histry` data from the Chirp end system and create `Immunization data` in it.

### 4. Vaxcare SAPI

The `health-vaxcare-sapi` module is a Mule application for processing healthcare data related to Vaxcare end system.

This system API facilitates the retrieval of `Patient appointment` and `Patient appointment` data from the Vaxcare end system.

The Vaxcare Mule system API connects to the backend of Vaxcare through a socket `send and receive` connector from Mule. By default, the socket connector is configured with a `safe protocol`, which Vaxcare does not accept. Additionally, this protocol is not recommended for production as it precedes every message with a cookie.

[Refer connector documentation](https://docs.mulesoft.com/sockets-connector/latest/sockets-documentation#SafeProtocol)

### 5. Visit EAPI

The `health-visit-eapi` module is a Mule application for processing healthcare data connecting to Drex, Chirp, Vaxcare System APIs.

This Experience API receives requests from the Visit end system and routes messages to the required system APIs, returning responses from the System API.

The Visit EAPI is responsible for creating `Immunization history` and retrieving `Patient Immunization`, `Patient Blood Test`, `Patient Insurance`, `Patient Appointment` data from System APIs.

# Health EHR Inventory API
 
## Overview
 
The `health-ehr-inventory-api` is Mule application that showcases the integration between a generic Inventory Management System (Inventory) and an Electronic Health Record (EHR) using MuleSoft.
 
The `health-ehr-inventory-api-flow` triggers the process at 9PM EST everyday where the flow will retrieve inventory data from a cloud-based relational database and send it to the EHR in JSON format.
 
Errors occured while connecting to Database or EHR system is retried for 3 times, if the error still persists the structured error response is logged.
 
## Setup

### Prerequisites

- Java JDK 8 or later
- Maven
- Mule Runtime
- Anypoint Studio

### Installation

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Build the project using Maven:

   ```bash
   mvn clean install
   ```

3. Open the project in Anypoint Studio (Optional):

   - Open Anypoint Studio
   - Import the project as an existing Mule project

## Deployment

### Local Deployment

1. Ensure Mule Runtime is installed and configured.
2. Deploy the application using Anypoint Studio or via command line:

   ```bash
   mule deploy
   ```

### CloudHub Deployment

1. Package the application using Maven:

   ```bash
   mvn clean package
   ```

2. Deploy the packaged application to CloudHub via Anypoint Platform.

## Configuration

### External Configuration Files

The project includes external configuration files located in `src/main/resources/config`. These configuration files manage different environments such as `local`, `dev`, and `common`.

- `local-config.yaml`
- `dev-config.yaml`
- `common.yaml`

### Global Configuration

The global configurations are defined in the `global.xml` file located in `src/main/mule`.

## Usage

### Running Tests

The project includes MUnit tests for various flows and functions. To run the tests, use the following command:

```bash
mvn clean test
```

### Accessing APIs

Each API module has its own endpoints and interfaces defined. Refer to the `interface.xml` files in the respective modules for detailed endpoint information.




# GitHub Actions Workflows for Mule Application

This repository contains GitHub Actions workflows for downloading, publishing, and deploying RAML files and Mule application modules.

## Workflows Overview

The main workflows are defined in separate YAML files within the `.github/workflows` directory. These workflows are modularized and include:

1. `main.yml` - The primary workflow that triggers other workflows based on the input parameters.
2. `download.yml` - Workflow for downloading RAML files from Anypoint Platform.
3. `upload.yml` - Workflow for uploading RAML files to Anypoint Platform.
4. `deploy.yml` - Workflow for deploying Mule application modules.

## Contributing

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.


