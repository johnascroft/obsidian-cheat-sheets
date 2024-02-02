# Committing deploy

Useful script for committing our deploy.sh script across multiple repositories.

```bash
#!/bin/bash

repositories=(
  "gps"
  "ces"
  "jigsaw"
  "reporting"
  "aerio"
  "wolfy"
)

deploy_script_path="/path/to/deploy.sh"

for repo_dir in "${repositories[@]}"; do
  # Copy the deploy.sh script to the repository
  cp "$deploy_script_path" "$repo_dir"

  # Navigate to the repository directory
  cd "$repo_dir"

	# Checkout main branch
	git checkout main

	# Get the latest changes before committing
  git pull

  # Add the deploy.sh script to the staging area
  git add deploy.sh

  # Commit the changes
  git commit -m "Add deploy.sh script"

  # Push the changes
  git push

  # Navigate back to the original directory
  cd -
done
```