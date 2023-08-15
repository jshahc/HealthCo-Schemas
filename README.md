# HealthCo Schema Management Guide

Welcome to the HealthCo Schema Management repository. This repository serves as a central hub for storing and managing
schemas for our cloud infrastructure. The schema management process is divided into two primary workflows: Pull Request
Workflow and Push Workflow.

## Pull Request Workflow

The Pull Request Workflow ensures that schemas are thoroughly validated and compatible before they are merged and
registered. This workflow involves the following steps:

1. **Schema Validation**: Ensure the correctness of the schema and its structure. The schema's subject name and path are
   to be provided for validation.

2. **Local Compatibility Test**: Test the compatibility of the new schema with existing schemas in the local
   environment. Provide details such as the location of existing schemas, the schema to be tested, compatibility level,
   and schema type.

3. **Set Compatibility Level**: Set the compatibility level for the subject. Specify the desired compatibility level.

4. **Cloud Compatibility Test**: Verify compatibility with the subject on the cloud. Provide subject name, compatibility
   level, and schema type for testing.

The `test local compatibility` goal can be utilized to confirm that the schema intended for publication is compatible
with the development environment locally. It's important to note that registration of development schemas on the cloud
is not necessary for this step. Ensure that the specified subject exists; otherwise, the workflow will fail.

## Push Workflow

The Push Workflow focuses on registering schemas once they have been validated and confirmed to be compatible. The
workflow encompasses the following stages:

1. **Schema Validation**: Ensure the correctness of the schema and its structure. The schema's subject name and path are
   required.

2. **Schema Registration**: Register the validated schema. Provide details such as the subject name, schema path, and
   schema type.

## Adding a Schema

To add a new schema to the repository, follow these steps:

1. Place the schema file in the `src/resources/prod/schemas` directory.
2. Update the `latestSchema` variable in the `pom.xml` file to reflect the changes.
3. Create a pull request with the updated schema.
4. Ensure that compatibility checks for the pull request pass before merging.

Upon merging the pull request, the schema will be automatically registered.

## Setup

Refer to
the [Schema Registry Maven Plugin documentation](https://docs.confluent.io/platform/current/schema-registry/develop/maven-plugin.html)
for comprehensive details about each goal. The arguments for each goal are defined in the `pom.xml` file.

### Important Reminders

1. Add the following secrets as GitHub actions: `SCHEMA_REGISTRY_URL`, `SCHEMA_REGISTRY_USERNAME`,
   and `SCHEMA_REGISTRY_PASSWORD`. These secrets are vital for the actions to function correctly. You can manage these
   secrets in the GitHub repository settings.

   ![GitHub Secrets](src/test/resources/GitHub_Secrets.png)

2. For the initial schema of a subject, direct registration without compatibility checks is necessary since the subject
   does not exist. In such cases, either merge the schema directly into the main branch or register the first schema
   using the UI/API. For more details, refer to
   the [Confluent Cloud Schema Registry Tutorial](https://docs.confluent.io/cloud/current/sr/schema_registry_ccloud_tutorial.html).

Thank you for your contributions to HealthCo's schema management. If you have any questions or need assistance, don't
hesitate to reach out to our team. Happy coding!
