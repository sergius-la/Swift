# XCUITest

Tools:
- Xcode -> Open developer tools -> `Accessibility Inspector`
    - <kbd>⌥ Alt</kbd> + <kbd>Space</kbd> - Inspect Element
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

#### XCUIApplication methods

- `.swipeDown()`, `.swipeLeft()`
    - swipe by coordinate

## XCUIElementQuery

#### XCUIElementQuery methods

- Element type: Button, table, menu, etc
    - `.descendantsMatchingType()`
    - `.childrenMatchingType()`
    - `.containingType()`
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

- `value`
- `.coordinate(withNormalizedOffset: CGVector(dx: 0, dy: 0))`

#### XCUIElement methods

- __Interactions:__
    - `XCUIElement.tap()`
    - ```swift
      // XCUIElement: textField - Type text
      let textField = app.textFields[<label/title>]
      textField.tap()
      textField.typeText(<text>)
      ```
    - ```swift
      // XCUIElement: pickerWheel - Set value
      let pickerWheel = app.pickerWheels[<label/title>]
      pickerWheel.adjust(toPickerWheelValue: <value>)
      ```
    - ```swift
      // XCUIElement: sliders - Set value
      app.sliders.element.adjust(toNormalizedSliderPosition: 0.7)
      ```
- __Verification:__
    - `.exists` -> boolean
    - `.isSelected` -> boolean