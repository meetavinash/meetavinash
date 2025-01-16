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
