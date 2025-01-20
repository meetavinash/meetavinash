Hello,

This is Avinash from India. I like to learn concepts and logics. I am not bound to Microsoft tech only but liked to do more with UI as well.
Learning Angular and design is my hobby.

Will bring some exciting demos here

Thank you
Avinash

# azure-pipelines.yaml
# ... other pipeline stages ...

- stage: CheckLoggerNames

  jobs:
  - job: CheckLoggerNamesJob

    steps:
    - task: Bash@3
      inputs:
        targetType: 'inline'
        script: |
          #!/bin/bash
          set -e # Exit immediately on error

          # Read logger names from configuration.yaml
          logger_names=$(yq e '.loggers | keys' configuration.yaml)

          # Define a regular expression for valid logger names
          valid_logger_regex='^[a-zA-Z0-9_.]+$'

          # Iterate over logger names and check for validity
          for logger_name in $logger_names; do
            if ! [[ $logger_name =~ $valid_logger_regex ]]; then
              echo "Invalid logger name: $logger_name"
              exit 1
            fi
          done

          echo "All logger names are valid."

# ... other pipeline stages ...


// In your custom linting functions file (e.g., custom-functions.js)

function has(target, functionOptions) {
  const { property, value } = functionOptions;

  if (property) {
    // Check if the property exists
    if (!target.hasOwnProperty(property)) {
      return {
        message: `Expected property '${property}' to be present.`,
      };
    }

    // If a value is specified, check if the property has the expected value
    if (value && target[property] !== value) {
      return {
        message: `Expected property '${property}' to have value '${value}'.`,
      };
    }
  } else {
    // If no property is specified, simply check if the target is not empty
    if (Object.keys(target).length === 0) {
      return {
        message: 'Expected target to not be empty.',
      };
    }
  }

  return null; // No issues found
}

module.exports = has;



rules:
  mandatory-header:
    given: $..request.headers
    then: function: has
    functionOptions:
      keys:
        - 'X-API-Key'
        - 'Authorization'
