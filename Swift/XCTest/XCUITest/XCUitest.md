# XCUITest

Tools:
- Xcode -> Open developer tools -> `Accessibility Inspector`
    - <kbd>⌘ Command</kbd> + <kbd>F7</kbd> - Inspect Element
- `UI Recorder`

***

```swift
import XCTest

// Test class extend - XCTestCase
class CalculatorUITests: XCTestCase { 
                            
    let app = XCUIApplication(bundleIdentifier: <app.name>) // Specify - bundleIdentifier if needed

    override func setUp() {
        super.setUp()
        continueAfterFailure = false
        app.launch()
    }
    
    override func tearDown() {
        super.tearDown()
    }
    
    // Test method starts with - test
    func testHelloWorld() {
        print("Hello World")
    }
}
```

## XCUIApplication

[_GitHub: Native App Bundle Identifiers_](https://github.com/joeblau/apple-bundle-identifiers)
- Settings: `com.apple.Preferences`
- App Store: `com.apple.AppStore`
- Safari: `com.apple.mobilesafari`

## XCUIElementQuery

#### XCUIElementQuery methods

- Element type: Button, table, menu, etc
    - .descendantsMatchingType()
    - .childrenMatchingType()
    - .containingType()
    ```swift
    let app = XCUIApplication()
    app.buttons[<"label">]

    // All buttons
    let buttons = app.buttons
    let allButtons = app.descendantsMatchingType(.Button)
    let childButtons = navBar.childrenMatchingType(.Button)

    let allCellsInTable = app.descendantsMatchingType(.Cell)
    let allMenuItemsInMenu = app.descendantsMatchingType(.MenuItem)
    ```
- Identifiers: Accessibility Identifier, label, title, etc
    ```swift
    // by Accessibility Identifier
    let element = app.buttons.matching(.button, identifier: "bt7").element
    let element = app.buttons.containing(.button, identifier: "bt8").element

    // by label
    let cellQuery = cells.containingType(.StaticText, identifier: "Groceries")
    ```
- Predicates: Value, partial matching, etc
    ```swift
    cell.buttons.matchingPredicate(NSPredicate(format: "label BEGINSWITH 'Delete'")).element
    ```

## XCUIElements

- Types:
    - buttons, staticTexts, switches, tables.cells, textFields, alerts
- Identifiers:
    - Accessibility identifier, label, title

#### XCUIElement attributes

- value

#### XCUIElement methods

- __Interactions:__
    - .tap()
    - .typeText(<"Text">)
- __Verification:__
    - .exists -> boolean
    - .isSelected -> boolean