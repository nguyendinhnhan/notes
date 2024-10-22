# Clean Swift 

## Project structure

For all iOS upcoming project to have standardized file structure, NFQ is standardized by following the below structure for Clean Swift Architecture. 

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
│   ├── Interactors
│   │   ├── [ModuleName]Interactor.swift
│   │   └── ...
│   ├── ViewModels
│   │   ├── [ModuleName]ViewModel.swift
│   │   └── ...
│   ├── Presenters
│   │   ├── [ModuleName]Presenter.swift
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
│   ├── Workers
│   │   ├── [ServiceName]Worker.swift
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
    ├── UnitTests
    │   ├── [ModuleName]
    │       ├── [ModuleName]InteractorTest.swift
    │       ├── [ModuleName]PresenterTest.swift
    │       ├── [ModuleName]RouterTest.swift
    │       ├── [ModuleName]ViewControllerTest.swift
    │       └── [ModuleName]Spy
    │           ├── [ModuleName]InteractorSpy.swift
    │           ├── [ModuleName]PresenterSpy.swift
    │           ├── [ModuleName]RouterSpy.swift
    └──         └── [ModuleName]ViewControllerSpy.swift
```

#### [UIModouleName]
This is the separate folder for bsic UI related things that we are going to use through out the project multiple times like PrimaryButton, SecondaryButton.
[Note]: Recommend to have separate external package rather than internal folder if possible. 

---

## Architecture

![](/iOS/Architecture/images/clean_swift.png "Clean Swift Architecture")

### ViewController (View)
The View is responsible for the user interface and user interactions. It should be as passive as possible, meaning it shouldn't contain complex business logic. Instead, it delegates user actions to the Presenter and displays data received from the Presenter.

### Interactor
The Interactor contains the application's business logic. It communicates with data sources, services, or repositories to retrieve and manipulate data. It should be independent of the UI and not have any UIKit dependencies. 

### Presenter
The Presenter acts as an intermediary between the ViewController and the Interactor. It receives data from the Interactor, formats it for presentation, and sends it to the View. 

### Router
The Router is responsible for navigation within the module and can be used for transitioning to other modules. It should not contain complex logic but should handle the assembly of the module and navigation.

### Models
Models are used to represent data and transfer it between components.

### DisplayModels
DisplayModels are used to present data from presenter to ViewController. It will not containes any extra data that are not needed to display in the UI, which makes the Unit testing to be more easy and independet with others. 

### Workers
Workers are used to handle network related staffs and communication with other modules. Workers are mainly exists inside interactor.

--- 

## Template 

Please download the template by clicking <a href="/iOS/Templates/CleanSwift.xctemplate.zip" download="CleanSwift.xctemplate.zip">here</a>.

Unzip the file and then copy it to the location: `/Users/[Name]]/Library/Developer/Xcode/Templates`

After that you can create new file using clean swift template.


![](/iOS/Architecture/images/create_clean_swift.png "Create clean swift template")
