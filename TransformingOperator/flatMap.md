# FlatMap

```swift
struct School {
    let name: String
    let noOfStudent: CurrentValueSubject<Int, Never>
    
    init(name: String, noOfStudnent: Int) {
        self.name = name
        self.noOfStudent = CurrentValueSubject(noOfStudnent)
    }
}

let citySchool = School(name: "Fountain Head School", noOfStudnent: 100)
let school = CurrentValueSubject<School, Never>(citySchool)

school.flatMap {
    $0.noOfStudent
}.sink { print($0) }

let townSchool = School(name: "Town Head School", noOfStudnent: 45)

school.value = townSchool

citySchool.noOfStudent.value += 1
townSchool.noOfStudent.value += 10
```
