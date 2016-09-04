# Load data into OpenSpending

It is possible to load Fiscal Data Packages into OpenSpending via a web app (the Packager) and via a CLI.

## Using the Packager

- [Code repo](https://github.com/openspending/os-packager)
- [Packager URL](http://next.openspending.org/packager)

The Packager provides a simple user interface to load data into OpenSpending. The app is a wizard that guides the user through the uploading of a data source, the modeling of a Fiscal Data Package, the provision of metadata, and publication to the OpenSpending Datastore.

## Using the CLI

- [Code repo](https://github.com/openspending/os-cli)
- [CLI docs](http://docs.openspending.org/en/latest/developers/cli/)

The CLI provides a simple command line interface to interact with an OpenSpending instance. Using the CLI, you can authenticate with an OpenSpending instance and then push data directly to the datastore.

## Walkthroughs

### Load data via the Packager

1. After assigning a DataType to each column in your file and packaging the data, you can proceed to step 3 of the data upload process.
![Image1](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/Step%203%20provide%20metadata.jpg)

2. At step 3 “Provide metadata,” name your dataset and provide metadata for better indexing. Include at least a Data Package name and a unique identifier.
![Image2](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/Metadata..jpg)

3. As soon as you provide the details about your data, you will get a message saying “Congratulations! Now you can verify your Data Package and download it”:
![Image3](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/step%203%20continue.jpg)

4. Click “Continue” to proceed to Step 4 to either “Download” the JSON file or “Publish this Data Package.”
![Image4](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/Step%204..jpg)

5. If you are logged in, you will be able to download or publish the data package. If not, you will be reminded to “Login to publish” before being able to move forward.
![Image5](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/login%20to%20publish..jpg)

6. Two bars will show the progress of publishing your data.
![Image6](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/publishing%20status..jpg)

7. Once your file was published, you can continue to exploring and visualizing your data in OS Viewer, by clicking “Explore and visualize your data now!”
![Image7](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/finalize.jpg)

8. If you want your data to be available to the larger audience, publish it from OS Admin. To access OS Admin, click on your name in the upper-right corner, and then click “Profile,” which will take you to OS Admin.

![Image8](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/click%20on%20name..jpg)

![Image9](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/click%20profile..jpg)

9. In the menu on the left of the screen, click “My datasets.”
![Image10](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/os%20admin..jpg)

10. You will be able to see the number of uploaded, published and hidden datasets.
![Image11](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/os%20admin1..jpg)

11. In OS Admin you have the ability to search your datasets, publish or unpublish a dataset. To finalize publishing, click “Publish” next to the dataset you want to make available.
![Image12](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/publish..jpg)

### Load data via the CLI

{
pre. start with two data sources, one good one bad, both already have an FDP.
1. check, validate, etc etc.
2. authenticate with the service.
3. Push files up.
4. Ping for API load status
}
