# ethereum-tests-xz

ethereum/tests repo but minified and compressed 

```bash
#!/bin/bash

# Check if 'jq' is installed
if ! command -v jq &> /dev/null; then
    echo "The 'jq' command could not be found. Please install 'jq' to use this script."
    exit 1
fi

# Function to minify JSON files
minify_json() {
    local file="$1"
    tmp_file=$(mktemp)
    if jq -c . "$file" > "$tmp_file"; then
        mv "$tmp_file" "$file"
        echo "Minified: $file"
    else
        echo "Failed to minify: $file"
        rm "$tmp_file"
    fi
}

# Export the function so it can be used by 'find' command
export -f minify_json

# Find and minify JSON files recursively from the current directory
find . -type f -name "*.json" -exec bash -c 'minify_json "$0"' {} \;

echo "JSON minification completed."
```

```bash
 XZ_OPT='-9' tar -cvJf ethereum-tests.xz /ethereum-tests
```
