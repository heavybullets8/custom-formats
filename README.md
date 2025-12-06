## Archival
The repo is to be archived as it is no longer required due to the upstream changes to **Recyclarr** in this release: 

https://github.com/recyclarr/recyclarr/releases/tag/v7.5.0

Specifically due to the new `resource_providers`, you can see my migration to using this with my custom formats in this commit:

https://github.com/heavybullets8/heavy-ops/commit/247f19b6d4f624a0cbaf4aec10a9377953495da7
---

# Slimmed Down TRaSH-Guides for Recyclarr

This repository is a **slimmed-down version** of the excellent [TRaSH-Guides](https://github.com/TRaSH-Guides/Guides) repository, specifically tailored for use with **Recyclarr** and my [**Talos Kubernetes cluster**](https://github.com/Heavybullets8/heavy-ops).

## **Purpose**

- **Automated Synchronization**: Syncs with the upstream repository [TRaSH-Guides](https://github.com/TRaSH-Guides/Guides) once per day via a GitHub Action.
- **Custom Formats Retention**: Retains my custom formats to ensure compatibility with my specific setup.
- **Public Repository**: Unfortunately **public** since Recyclarr does not support private repositories at this time.

## **Usage**

### **Forking the Repository**

If you wish to use this repository for your own setup, you can **fork** it:

1. Click the **Fork** button at the top right of this page to create your own copy of the repository.
2. Clone your forked repository to your local machine.

### **Configuring `config.yaml`**

The `config.yaml` file is the core configuration file that defines which paths and files are synchronized from the upstream repository. Here's how it's structured and how you can customize it:

```yaml
radarr:
  custom_formats:
    path: "docs/json/radarr/cf"
    exclude:
      - "custom-format1.json"
      - "custom-format2.json"
  qualities:
    path: "docs/json/radarr/quality-size"
  naming:
    path: "docs/json/radarr/naming"
    exclude:
      - "custom-naming-file-example-1.json"
      - "custom-naming-file-example-2.json"
  quality_profiles:
    path: "docs/json/radarr/quality-profiles"
  custom_format_groups:
    path: "docs/json/radarr/cf-groups"
    exclude:
      - "custom-format-group-1.json"

sonarr:
  custom_formats:
    path: "docs/json/sonarr/cf"
    exclude:
      - "custom-format1.json"
      - "custom-format2.json"
  qualities:
    path: "docs/json/sonarr/quality-size"
  naming:
    path: "docs/json/sonarr/naming"
    exclude:
      - "custom-naming-file-example-1.json"
      - "custom-naming-file-example-2.json"
  quality_profiles:
    path: "docs/json/sonarr/quality-profiles"
  custom_format_groups:
    path: "docs/json/sonarr/cf-groups"
    exclude:
      - "custom-format-group-1.json"

additional_sync:
  - "docs/Radarr/Radarr-collection-of-custom-formats.md"
  - "docs/Sonarr/sonarr-collection-of-custom-formats.md"
  - "metadata.json"
```

#### **Key Sections**

- **`radarr` and `sonarr`**: These sections define the paths for various configurations and custom formats for Radarr and Sonarr. Each subkey (e.g., `custom_formats`, `qualities`, etc.) contains:

  - **`path`**: The directory path where the files for that subkey are located.
  - **`exclude` (optional)**: A list of filenames to **exclude** from synchronization. This prevents your custom files from being overwritten during the sync process.

- **`additional_sync`**: Specifies additional files to synchronize from the upstream repository. By default, it includes files required by Recyclarr to verify the repository.

#### **Customizing Your Configuration**

##### **Adding Custom Files**

To retain your custom formats or configurations:

1. **Place Your Custom Files**: Put your custom JSON files in the appropriate directories as specified by the `path` under each subkey.

   - For Radarr custom formats: `docs/json/radarr/cf/`
   - For Sonarr custom formats: `docs/json/sonarr/cf/`
   - For other subkeys, use the paths specified in the `config.yaml`.

2. **Specify Files to Exclude**: Add the filenames of your custom files to the `exclude` list under the relevant subkey in the `config.yaml`. This ensures they are **excluded** during the synchronization process and not overwritten.

##### **Example: Adding a Custom Format to Radarr**

If you have a custom format file for Radarr called `my-custom-format.json`, follow these steps:

1. **Place the File**:

   - Put `my-custom-format.json` in the directory specified by the `path` for `custom_formats`:

     ```
     docs/json/radarr/cf/my-custom-format.json
     ```

2. **Update `config.yaml`**:

   ```yaml
   radarr:
     custom_formats:
       path: "docs/json/radarr/cf"
       exclude:
         - "my-custom-format.json"
     # ... other subkeys ...
   ```

##### **Example: Excluding Custom Naming Files in Sonarr**

If you have custom naming files for Sonarr:

1. **Place the Files**:

   - Put your custom naming files in `docs/json/sonarr/naming/`.

2. **Update `config.yaml`**:

   ```yaml
   sonarr:
     naming:
       path: "docs/json/sonarr/naming"
       exclude:
         - "my-custom-naming.json"
     # ... other subkeys ...
   ```

### **Running the Synchronization**

The repository is set up to automatically synchronize with the upstream TRaSH-Guides repository once per day using GitHub Actions. However, if you want to trigger the synchronization manually:

1. Go to the **Actions** tab in your repository on GitHub.
2. Select the **"Sync Custom Formats from Upstream"** workflow.
3. Click on **"Run workflow"** and select the branch you want to run it on.

### **Notes**

- **Directory Structure**: Ensure that any new files you add are placed in the correct directories as specified in the `path` values in the `config.yaml` file.
- **Custom Exclusions**: The `exclude` lists use filenames, not full paths. The script will exclude these files from synchronization in their respective directories.
- **Upstream Changes**: If the upstream repository changes its directory structure, the GitHub Action is designed to handle such changes by updating the paths and moving files accordingly. Since the `exclude` lists are associated with subkeys and use filenames, your custom files remain protected even if paths change.
- **Additional Files**: You can add more files to the `additional_sync` list if you need to synchronize specific files from the upstream repository.

## **Credits**

All credit for the guides and original content goes to the [TRaSH-Guides](https://github.com/TRaSH-Guides/Guides) repository. This repository is simply a tailored version meant to suit my personal needs.

## **Disclaimer**

This repository is intended for **personal use**. If you choose to fork and modify it, please ensure you comply with the licensing terms of the original [TRaSH-Guides](https://github.com/TRaSH-Guides/Guides) repository.

## **Contributing**

Contributions are welcome if they align with the purpose of this repository. However, please note that this is a personal project, and changes may not be merged if they do not fit my specific use case.
