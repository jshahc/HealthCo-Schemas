# HealthCo

Repository to store and manage schemas for our cloud. There are 2 workflows:

1. pull-request: validate schema, test compatibility locally and with subject
2. push: register schema with schema registry

## Adding a Schema

1. Add the file to `src/resources/prod/schemas`, update the `latestSchema` variable in  `pom.xml` and create a PR.
2. Make sure the compatibility checks for the PR pass before merging.
3. On merging the PR, the schema would be registered.

## Setup

Follow [Schema Registry Maven Plugin](https://docs.confluent.io/platform/current/schema-registry/develop/maven-plugin.html)
for details on each goal. The arguments for each goal is defined in the `pom.xml` file.

### Pull-Request Workflow

[This workflow](.github/workflows/pull-request.yaml) does the following:

1. Validates the schema. (Subject name and path of schema is to be provided)
2. Tests compatibility locally with existing schemas. (Location of existing schemas, schema to test, compatibility level
   and schema type is to be provided)
3. Sets compatibility for subject. (compatibility level is to be provided)
4. Tests compatibility with subject on cloud. (Subject name. compatibility level and schema type is to be provided)

Test local compatibility goal can be used to verify that the schema to be published is compatible with dev environment
locally. You don't need to register the dev schemas on the cloud. Please make the sure the subject exists else this
workflow would fail.

### Push Workflow

[This workflow](.github/workflows/push.yaml) does the following:

1. Validates the schema. (Subject name and path of schema is to be provided)
2. Registers the schema. (Subject name, path of schema and schema type is to be provided)

### Points to Remember

1. Add the `SCHEMA_REGISTRY_URL`, `SCHEMA_REGISTRY_USERNAME` and `SCHEMA_REGISTRY_PASSWORD` as secrets for GiHub
   actions.
   ![img.png](src/test/resources/GitHub_Secrets.png)
2. The first schema for a subject should be registered directly without compatibility checks because the subject doesn't
   exist. So, the pull-request workflow would fail. Hence, merge schema directly to main branch or register the first
   schema
   using the UI/API. [Reference](https://docs.confluent.io/cloud/current/sr/schema_registry_ccloud_tutorial.html)



