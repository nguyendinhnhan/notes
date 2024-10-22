# MVVM R

## Project structure

For all iOS upcoming project to have standardized file structure, NFQ is standardized by following the below structure for MVVM. 

```
[Project Name]
├── [Project Name]
│   ├── AppDelegate.swift
│   ├── SceneDelegate.swift
│   ├── Main.storyboard
│   ├── Assets.xcassets
│   └── Info.plist
├── [UIModouleName] 
│   ├── CustomViews
│   │   ├── [CustomName]View.swift
│   │   └── ...
│   ├── BasicComponents
│   │   ├── TextFields
│   │   │   ├── [ProjectName]TextField.swift // NFQTextField
│   │   │   └── ...
│   │   ├── Buttons
│   │   │   ├── [ProjectName]PrimaryButton.swift // NFQPrimaryButton
│   │   │   ├── [ProjectName]SecondaryButton.swift // NFQPrimaryButton
│   │   │   └── ...
│   │   └── ...
├── [ModuleName]
│   ├── ViewModel
│   │   ├── [ModuleName]ViewModel.swift
│   │   └── ...
│   ├── Views
│   │   ├── [ModuleName]ViewController.swift
│   │   ├── [ModuleName]View.xib
│   │   └── ...
│   ├── Models
│   │   ├── [ModuleName].swift
│   │   └── ...
│   ├── Routers
│   │   ├── [ModuleName]Router.swift
│   │   └── ...
│   ├── Services
│   │   ├── [ServiceName]Service.swift
│   │   └── ...
├── Utils
│   ├── Extensions
│   │   └── ...
│   ├── Helpers
│   │   └── ...
│   └── Constants.swift
├── Resources
│   ├── Assets
│   │   ├── Images
│   │   └── Icons
│   ├── Localization
│   └── Fonts
└── Tests
    └── UnitTests

```

#### [UIModouleName]
This is the separate folder for bsic UI related things that we are going to use through out the project multiple times like PrimaryButton, SecondaryButton.

[Note]: Recommend to have separate external package rather than internal folder if possible. 

---

## Architecture

![](/iOS/Architecture/images/mvvm_r.png "MVVM Architecture")

### Model: 
Represents the data and business logic of the application. It is responsible for data manipulation, retrieval, and storage.

### ViewController (View)
Represents the user interface elements of the application. It is responsible for displaying data and capturing user input.

### ViewModel 
Acts as an intermediary between the Model and the View. It contains the presentation/business logic and exposes data and commands that the View can bind to.

### Router
Manages the navigation and flow of the application. It decides which View to display and how to transition between Views.

### Service
Services are  used to handle network related staffs and communication with other modules. Services are mainly exists inside ViewModel.

--- 

## Template 

Please download the template by clicking <a href="/iOS/Template/MVVM.xctemplate.zip" download="MVVM.xctemplate.zip">here</a>.

Unzip the file and then copy it to the location: `/Users/[Name]]/Library/Developer/Xcode/Templates`

After that you can create new file using MVVM template


![](/iOS/Architecture/images/create_mvvm.png "Create MVVM R template")
