# TableView-Bindings
Memo Cocoa Bindings TableView

*Aufgabe*: Erstelle das Modell `Person` – eine Klasse aus Vor- und Nachnamen – die automatisch seinen Inhalt in die Tabelle einträgt.

<img src="https://lh3.googleusercontent.com/pw/ACtC-3fdkmPepZzzXf8U-bY-eNwhYIY_Y70K_YagPZSqkFgpRDqLHtPjUWz8OaVklmpiR8gu7-Xp9bvtUhFaJuMlhGdSoaQhuPpm7Q461qHzjkO9Q7WNlDbthSxab0KcEdP6ZET5eKSsPHDRRB5dmu0rxRKB=w1184-h808-no?authuser=0" width=480>

<center><font size=7>⚙︎⚙︎⚙︎</font></center>

*Lösung*:

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

* Notiere die Namen «firstName» und «lastName». Die brauchen wir für die Bindings.

```swift
import Cocoa

class ViewController: NSViewController {
    
    @objc dynamic var employees = [Person]()

    override func viewDidLoad() {
        super.viewDidLoad()
        DispatchQueue.global(qos: .userInteractive).async {
            let persons = self.loadStaff()
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

* Notiere den Namen «employees». Wir brauchen ihn für die Bindings.

---

* Setze ein *Table View* auf das *View* des *View Controllers*.
* Setze einen *Array Controller* auf die Leiste über dem *View Controller*:
	<img src="https://lh3.googleusercontent.com/pw/ACtC-3fBwrO5jIAFY5MAl_5IIzdNcyFXLJf3dYqyFIozDGDfIMkr1ug3KXLoArueMoPt1lEpHEnbGBapj_gKszsOY0xrhnsewuKEtlBdgh0thW1tZoQB0YchX57_6hrZ4ylRJvppHxjBnRbrF0_wxCdCrXwz=w1012-h868-no?authuser=0" width=480>
* Im *Bindings Inspector*:
	* **Array Controller**: *Content Array* ▶︎ *Bind to View Controller*, *Model Key Path*: «self.employees»
	* **Table View**: *Table Content* ▶︎ *Bind to Array Controller*
	* **1. Table View Cell**: *Value* ▶︎ *Bind to Table Cell View*, *Model Key Path*: «objectValue.firstName»
	* **2. Table View Cell**: *Value* ▶︎ *Bind to Table Cell View*, *Model Key Path*: «objectValue.lastName»
