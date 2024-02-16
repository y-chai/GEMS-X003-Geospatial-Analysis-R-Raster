<img src="images/GEMS Informatics Learning.png" width=600 alt="GEMS Learning Logo" title="GEMS Learning" />

# X003.0 An Introduction to Spatial Data Analysis in R

This course is designed for those who are interested in explicitly accounting for location in their analyses. Through this 3-week introductory course, you will learn how to work with spatial data in R, starting from importing different spatial datasets and creating simple maps, to conducting basic geocomputation on vector and raster data. In each 2.5 hour lecture, you will have the opportunity to immediately practice your new skills via hands-on exercises focused on agri-food applications. 

- Week 1: Introduction to spatial data and mapping in R
- Week 2: Basic geocomputation with vector data in R
- Week 3: Basic geocomputation with raster data in R 

## Prerequisites: 
- Access to the internet
- Introductory knowledge of R & RStudio  

## Initial Setup
We will be teaching the entire course with RStudio, you will need to have R (version ≥ 4.3.0) and RStudio (version ≥ 2021.09) installed on your own machine to participate. If you are running outdated versions of either of these software, please ensure you update your software.

1. Launch RStudio. 
2. Install packages needed for course. If you have any issues please let your TA know immediately. 
    ```shell
    #list of necessary packages 
    necPkgs <- c('sf','terra','tmap','geodata')
    
    # list of all packages installed 
    allPkgsInst <- data.frame(
      Package = names(utils::installed.packages()[, 3]),
      Version = unname(utils::installed.packages()[, 3]),
      Depends = unname(utils::installed.packages()[, 5])
    )

    # list of necessary packages installed 
    necPkgsInst <- allPkgsInst[grep(paste0("^", necPkgs, "$", collapse = "|"),
                                    allPkgsInst["Package"][[1]]), ]
    
    # loop to either install or update necessary packages
    # load packages after install or update check
    for (pkg in necPkgs) {
    
      # if not installed, install
      if (!pkg %in% necPkgsInst$Package) {
        message(pkg, " is not installed. Installing now.")
        utils::install.packages(pkg, 
                                dependencies = TRUE)
      }
      # if installed, update
      else {
        if(pkg %in% old.packages()[, 1]) {
          message(pkg, " is installed, but newer version is available. Updating now.")
        }
        else {
          message(pkg, " is installed and up-to-date.")
        }
        
        # ask = false stops prompt for all updates
        utils::update.packages(oldPkgs = necPkgs, 
                               ask = FALSE)
      }
      
      # if not loaded, load
      if (!pkg %in% (.packages())) {
        library(pkg, character.only = TRUE)
      }
    }
    
    # verify necessary packages loaded successfully
    (.packages())
    ```
3. Download the data and scripts from Github by clicking on the green `<> Code` button and then the `Download ZIP` option.
4. Create a sub-directory folder named `~/GEMSX003` in a directory location of your choosing (e.g., Desktop, Documents, Google Drive, etc.).
5. Extract the contents of the downloaded zipped folder into your working directory folder. For consistency, the course contents should be stored under a sub-directory folder with the name of the Github repo. For example, `~/GEMSX003/GEMS-X003-Geospatial-Raster-R-Vector-main`. This folder will be referred to as the ***working directory***.
6. Set your working directory within RStudio. Use the menu to change your working directory under **Session > Set Working Directory > Choose Directory**. Choose the directory you unzipped your downloaded files to above with a name that matches the relevant Github repo. For example, `~/GEMSX003/GEMS-X003-Geospatial-Analysis-R-Raster-main`.
