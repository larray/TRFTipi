# TRF Tipi apps

This repository is the base for a collection of RunTipi App definitions used at TRF. 

## Repository Structure Notes

In keeping with the RunTipi Documentation I am maintaining the information related to how an app should be architected. Note: If you create the application in RunTipi and wish to port it to your personal App Store - the structure for these appear to be in your RunTipi instance at:

**~/runtipi/apps/_user**

After zipping each directory (zip -f folder.zip folder/) that I wanted to preserve, I exported them via SFTP and then extracted the contents to apps/appname. I then executed from CMD (del /s docker-compose.generated.yml) to purge all of the runtime generated YML files. 

- **apps/**: Contains individual app directories

  - Each app has its own folder (e.g., `whoami/`) with the following structure:
    - `config.json`: App configuration file
    - `docker-compose.json`: Docker setup for the app
    - `metadata/`: Contains app visuals and descriptions
      - `description.md`: Markdown description of the app
      - `logo.jpg`: App logo image

- **tests/**: Contains test files for the app store

  - `apps.test.ts`: Test suite for validating apps

## Getting Started

This repository is intended to serve as a template for creating your own app store. Follow these steps to get started:

1. Click the "Use this template" button to create a new repository based on this template
2. Customize the apps or add your own app folders in the `apps/` directory
3. Test your app store by using it with Runtipi

## Documentation

For detailed instructions on creating your own app store, please refer to the official guide:
[Create Your Own App Store Guide](https://runtipi.io/docs/guides/create-your-own-app-store)
