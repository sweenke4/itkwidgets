# How to:

## 1) Build `itkwidgets` to allow for changes to be made to `itk-vtk-viewer`

```bash

#!/bin/zsh

echo "\n**** Ensure that the correct conda environment is running **** \n"
conda deactivate
conda activate Jupyter_Scikit_VTK_3813

echo "\n**** Set the Home folder to work from **** \n"
PROJECTS="/Users/sweenke4/OneDrive - Novartis Pharma AG/Projects"

echo "\n**** Remove old versions of the folders to ensure we are starting from scratch **** \n"
cd -- "$PROJECTS"
rm -r -f itkwidgets
rm -r -f itk-vtk-viewer

## ----- ITK-VTK-VIEWER -----

echo "\n**** Clone in the itk-vtk-viewer repo and checkout the correct version **** \n"
cd -- "$PROJECTS"
git clone https://github.com/sweenke4/itk-vtk-viewer.git
cd itk-vtk-viewer
git checkout v10.7.4


## ----- ITKWIDGETS -----

echo "\n**** Clone in the itkwidget repo and checkout the correct version **** \n"
cd "$PROJECTS"
git clone https://github.com/sweenke4/itkwidgets.git
cd itkwidgets
git checkout v0.32.0 

echo "\n**** Install the itkwidgets package in development mode **** \n"
python -m pip install -e .

jupyter nbextension install --py --symlink --sys-prefix itkwidgets
jupyter nbextension enable --py --sys-prefix itkwidgets
jupyter nbextension enable --py --sys-prefix widgetsnbextension

echo "\n**** Update the location of the itk-vtk-viewer module to use within `package.json` and install it **** \n"
cd js

## ----- STOP!!!!! -----
## ADD these to package.json dependancies
## ---------------------

    # "@thewtex/iconselect.js": "^2.1.2",
    # "eventemitter3": "^4.0.4",
    # "mousetrap": "^1.6.5",


npm install --save ../../itk-vtk-viewer
npm install
npm run build

```

## 2) Make changes to `itk-vtk-viewer` and allow them to be implemented and visible in `Latent Explorer Tool`
