# TableView-Bindings

Use bindings in a MacOS application.

*Task*: A table should reflect the contents of a `Person`-object. `Person` should be a class consisting of two properties: `firstName: String` and `lastName: String`.

<img src="https://github.com/andreas1724/TableView-Bindings/blob/master/Screen%20Shot%202020-06-13%20at%2023.15.00.png" width=480>

---

*Solution*:

```swift
import Foundation

class Person: NSObject {
    @objc dynamic var firstName: String
    @objc dynamic var lastName: String
    
    init(firstName: String, lastName: String) {
        self.firstName = firstName
        self.lastName = lastName
    }
}
```

* Remember «firstName» and «lastName»!

```swift
import Cocoa

class ViewController: NSViewController {
    
    @objc dynamic var employees = [Person]()

    override func viewDidLoad() {
        super.viewDidLoad()
        DispatchQueue.global(qos: .userInteractive).async {
            let persons = self.loadStaff() // might be time consuming
            DispatchQueue.main.async {
                self.employees = persons
            }
        }
    }
    
    func loadStaff() -> [Person] {
        return [
            Person(firstName: "Peter", lastName: "Lustig"),
            Person(firstName: "Fritz", lastName: "Fuchs")
        ]
    }
}
```

* Remember «employees»!

---

* Drop a *Table View* onto the *View* of *View Controller*.
* Drop an *Array Controller* onto the bar above the *View Controller*:
	<img src="https://github.com/andreas1724/TableView-Bindings/blob/master/Screen%20Shot%202020-06-13%20at%2021.11.00.png" width=480>
* Use *Bindings Inspector*:
	* **Array Controller**: *Content Array* ▶︎ *Bind to View Controller*, *Model Key Path*: «self.**employees**»
	* **Table View**: *Table Content* ▶︎ *Bind to Array Controller*
	* **1. Table View Cell**: *Value* ▶︎ *Bind to Table Cell View*, *Model Key Path*: «objectValue.**firstName**»
	* **2. Table View Cell**: *Value* ▶︎ *Bind to Table Cell View*, *Model Key Path*: «objectValue.**lastName**»
