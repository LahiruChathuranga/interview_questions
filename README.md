# interview_questions

Question 1
Question 1 of 17
```swift
What do you like most about developing mobile Apps? What things don't you like about developing mobile apps?
So the first thing if we know about mobile app developments , we can make our own apps if we have any idea. so that is the main thing.
and when it comes to development side, 
mainly i like the process of developments. such as architechture, Solid, unit testing.
i don't like to work on garbage codes, if there is anything which are seems to be garbage, i will need to change them.
```

Question 2
Question 2 of 17

Complete the implementation of the following Swift function.

func doStuff() {
  let array: [String] = ["one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten"]
   
  // Print out array in alphabetical order
  <your-code-goes-here>

 // Print out the array in reverse numerical order
 <your-code-goes-here>

 // Print out all the array elements that start with the letter 't'
 <your-code-goes-here>

 // Print out a dictionary of elements grouped by the first letter
 <your-code-goes-here>
}
```Swift
// Print out array in alphabetical order
let sortedArray = array.sorted()
print(sortedArray)

// Print out the array in reverse numerical order
// var newArray = array
print(newArray.reverse())

 // Print out all the array elements that start with the letter 't'
 for element in array {
     if firstLetter = element.first, firstLetter.lowercased() == "t" {
         print(element)
    }
}
// Print out a dictionary of elements grouped by the first letter
let groupedDict = array.reduce(into: [String: [String]]()) {result, element in 
let firstLetter = String(element.prefix(1).lowercased())
result[firstLetter, default: []].append(element)
}

print(groupedDict)
```

Question 3
Question 3 of 17

Complete the implementation of the following Swift function.

func doStuff() {
  let dict = [1:"one", 2:"two", 3:"three", 4:"four", 5:"five", 6:"six", 7:"seven", 8:"eight", 9:"nine", 10:"ten", 11:"eleven", 12:"twelve", 13:"thirteen"]
 
  // Print out the keys of all the odd numbered entries in descending order
  <your-code-goes-here>
 
  // Print out the values of all even numbered entries that start with the letter 't'
  <your-code-goes-here>
 
  // Print out all the values that are multiples of 3
  <your-code-goes-here>
}
```swift
// Print out the keys of all the odd numbered entries in descending order
let oddKeys = dict.keys.filter { $0 % 2 != 0}
let sortedOddKeys = oddKeys.sorted(by: >)
print(sortedOddKeys)

// Print out the values of all even numbered entries that start with the letter 't'
let evenNumberEntries = dict.filter({$0.keys % 0 == 0 && $0.first.lowercased() == "t"})
print(evenNumberEntries.values)

// Print out all the values that are multiples of 3
  let multiplesOfThree = dict.filter ({$0.keys % 3 == 0})
  print(multiplesOfThree.values)

```
Question 4
Question 4 of 17

Given the following enumeration, write a Swift function to convert an integer to Roman numerals, e.g. 2018 = MMXVIII, 2019 = MMXIX, 2020 = MMXX. 

enum RomanAlphabet: Int, CaseIterable {
  case I=1, V=5, X=10, L=50, C=100, D=500, M=1000, W=5000, Y=10000
}

Using your function what is 12345 in Roman numerals?
```swift
func convertToRoman(_ number: Int) {
    var num = number
    var result = ""
    
    for romanCase in RomanAlphabet.allCases.sorted(by: {$0.rawvalue > $1.rawValue}) {
        while num >= romanCase.rawValue {
            result += "\(romanCase)"
            num -= romanCase.rawValue
        }
    }
    return result
}
12345 = "MMMMMMMMMMMMCCCXLV"
```

Question 5
Question 5 of 17

Write a Swift protocol for an Animal protocol that has properties for:

- name,
- color,
- number of legs
- number of wings
- has a tail or not

This protocol must also have methods that allow the type to:
- walk a certain distance
- fly a certain distance
- swim a certain distance

Provide default implementations for the three methods in the protocol, that throw error if the methods (walk/fly/swim) are called on an Animal that cannot walk, fly or swim.
```swift
protocol AnimalProtocol {
    var name: String { get }
    var color: String { get }
    var numOfLegs: Int { get }
    var numberOfWings: Int { get }
    var hasATailOrNot: Bool { get }
    
    func walkACertainDistance()
    func flyACertainDistance()
    func swimACertainDistance()
}
extension AnimalProtocol {
    func walkACertainDistance() {
        if numOfLegs == 0 {
            // throw error here
        }
    }
    func flyACertainDistance() {
        if numberOfWings == 0 {
            // throw error here
         }
    }
    func swimACertainDistance() {
        if hasATailOrNot {
            // throw error here
        }
    }
}
```

Question 6
Question 6 of 17

The Animal class has the following constraints:

- Animals must have an even number of legs or wings
- Animals may not have more than 8 legs or more than 6 wings
- Animals can fly if they have 2 or more wings
- Animals can walk if they have 2 or more legs
- Animals may not have a negative number of legs or wings

Write a unit test class using XCTest that validates the implementation of the above constraints.
```swiift
Class AnimalTests: XCTestCase {
    
    func testEvenNumberOfLegsOrWings() {
        let animal = Animal(legs: 4, wings: 2)
        XCTAssertTrue(animal.legs % 2 == 0 || animal.wings % 2 == 0)
    }
    
    func testmaxLegsAndWings() {
        let animal = Animal(legs: 4, wings: 2)
        XCTAssertTrue(animal.legs <= 8 || animal.wings <= 6)
    }
    
    func testCanFlyWithTwoWings() {
        let animal = Animal(legs: 4, wings: 2)
        XCTAssertTrue(animal.wings >= 2)
    }
    
    func testcanWalk() {
        let animal = Animal(legs: 4, wings: 2)
        XCTAssertTrue(animal.legs >= 2)
    }
    
    func testNoNegativeLegsOrWings() {
        let animal = Animal(legs: -2, wings: 0)
        XCTAssertGreaterThanOrEqual(animal.legs, 0)
        XCTAssertGreaterThanOrEqual(animal.wings, 0)
    }
}
```

Question 7
Question 7 of 17

Write a Swift extension to String that hyphenates all words in the string so that the expression:

"this is a string".hyphenate()

returns the value:

"t-h-i-s i-s a s-t-r-i-n-g"
```swift
extension String {
    func hypernate() -> String {
        var dashedString = ""
        for char in self {
            dashedString.append(char)
            dashedString.append("-")
        }
        
        dashedString.removeLast() // last dash removed
        
        return dashedString
    }    
}

```
Question 8
Question 8 of 17

Write a function called makePrinter() that takes an array of Strings, and returns a function that will print out each of those elements when it is called.

So given the code:

let myFunction = makePrinter(["one", "two", "three"])
myFunction()
 
// will print the following output:
// one
// two
// three
```swift
func makePrinter(arr: [String]) -> () -> Void {
    
    func printItems() {
        arr.map({print($0)})
    }
    
    return printItems()

}
```

Question 9
Question 9 of 17

Write a function called makeRepeater(nTimes: Int), that returns a function that takes a string and prints out that string nTimes. So the code:

let myFunction = makeRepeater(3)
myFunction("Hello World")
 
// will print out:
// Hello World
// Hello World
// Hello World
```swift
func makeRepeater(_ count: Int) -> (String) -> Void {
    func printer(_ input: String) {
        for _ in 0...count {
            print("\(input)\n")
        }
    }
    
    return printer
}
```

Question 10
Question 10 of 17

Complete the implementation below:

enum ValidationError: Error {
  case invalidPassword
  case passwordNotMatch
  case otherError
}
 
func validate(element: String, _ validator: (String) throws -> ()) {
  do {
    try validator(element)
  } catch let err {
    print(err)
  }
}
 
// Write a password validator function named passwordValidator that can be pass into validate(element, _) so that calling the validate function with password and passwordValidator will throw a ValidationError if the password is not valid.
// A valid password must have length of between 8 and 13 characters and the characters must be alphanumeric and case sensitive.
func passwordValidator() -> (String) throws -> Void {
  <your-code-goes-here>
}
 
// Test your validator
<your-code-goes-here>
 
// Write a password confirmation validator function named passwordConfirmValidator that can be passed into validate(element, _) so that calling the validate function with password and passwordConfirmValidator will throw a ValidationError if the password does not match the confirm password expression.
func passwordConfirmValidator(value: @escaping @autoclosure () -> String) -> (String) throws -> Void {
  <your-code-goes-here>
}
 
// Test your validator
<your-code-goes-here>
```swift
func passwordValidator() -> (String) throws -> Void {
    return { password in
            guard password.count >= 8, password.count <= 13 else {
                throw ValidationError.invalidPassword
            }
            
            let alphanumericCharacterSet = CharacterSet.alphanumerics
            guard password.rangeOfCharacter(from: alphanumericCharacterSet.inverted) == nil else {
                throw ValidationError.invalidPassword
            }
            
            print("Password is valid.")
        }
}

let passwordvalidator = passwordValidator()
validate(element: "212121", passwordvalidator)

func passwordConfirmValidator(value: @escaping @autoclosure () -> String) -> (String) throws -> Void {
    return { confirmPassword in
        let originalPassword = value()
        
        guard confirmPassword == originalPassword else {
            throw ValidationError.passwordNotMatch
        }
        
        print("Password confirmation is valid.")
    }
}

let password = "1234567"
let confirmPassword = "123456789"

let result = validate(element: confirmPassword, passwordConfirmValidator(value: password))

switch result {
case .success:
    print("Validation successful")
case .failure(let error):
    print("Validation failed with error: \(error)")
}

```



Question 11
Question 11 of 17

Given the following JSON:

{
  "memberProfile": {
    "memberSystemId": "63c2fe23-90a1-489f-a372-a249a616f1ee",
    "preferredName": "John Doe",
    "email": "john.doe@test.com",
    "emailVerified": true,
    "dateOfBirth": "1957-08-31",
    "sequenceId": 5,
    "mailingAddress": {
      "address1": "Level 11",
      "address2": "199, Jalan Tun Razak",
      "city": "Kuala Lumpur",
      "country": "Malaysia",
      "postcode": "50450"
    },
    "favColor": "#b20040"
  }
}

// Complete the implementation below:

struct MemberAddress: Codable {
  <your-code-goes-here>
}
 
struct MemberProfile: Codable {
  var memberSystemId: String
  var name: String
  var email: String
  var emailVerified: Bool
  var dateOfBirth: Date?
  var sequenceId: Int
  var address: MemberAddress?
  var favColor: UIColor?
 
  <your-code-goes-here>
}
 
struct MemberProfileResponse: Codable {
  var memberProfile: MemberProfile
 
  static function decoder() -> JSONDecoder {
    <your-code-goes-here>
  }
}
```swift
struct MemberAddress: Codable {
  var address1: String?
  var address2: String?
  var city: String?
  var country: String?
  var postcode: String?
}
struct MemberProfile: Codable {
  var memberSystemId: String
  var name: String
  var email: String
  var emailVerified: Bool
  var dateOfBirth: Date?
  var sequenceId: Int
  var address: MemberAddress?
  var favColor: UIColor?
 
 init(from decoder: Decoder) throws {
        let container = try decoder.container(keyedBy: CodingKeys.self)
        
        memberSystemId = try container.decode(String.self, forKey: .memberSystemId)
        name = try container.decode(String.self, forKey: .name)
        email = try container.decode(String.self, forKey: .email)
        emailVerified = try container.decode(Bool.self, forKey: .emailVerified)
        dateOfBirth = try container.decodeIfPresent(Date.self, forKey: .dateOfBirth)
        sequenceId = try container.decode(Int.self, forKey: .sequenceId)
        address = try container.decodeIfPresent(MemberAddress.self, forKey: .address)
        favColor = try container.decodeIfPresent(UIColor.self, forKey: .favColor)
    }
  
}

struct MemberProfileResponse: Codable {
  var memberProfile: MemberProfile
 
  static func decoder() -> JSONDecoder {
    return JSONDecoder()
  }
}
```

Question 12
Question 12 of 17

struct MemberProfile: Codable {
  var memberSystemId: String
  var name: String
  var email: String
  var emailVerified: Bool
  var dateOfBirth: Date?
  var sequenceId: Int
  var address: MemberAddress?
  var favColor: UIColor? 
}

Given an array of MemberProfile (from Question 11) and using only higher order functions like Map, Filter, Reduce, etc., return an NSAttributedString object that contains the members' names in system font with font colour of favColor, ordered by the sequenceId. For every even numbered element in the array, include the members' email address in parenthesis after the members' name.
```swift
let memberProfiles: [MemberProfile] = []

let attributedString: NSAttributedString = memberProfiles
    .sorted { $0.sequenceId < $1.sequenceId }
    .enumerated()
    .map { (index, member) -> NSAttributedString in
        let nameAttributes: [NSAttributedString.Key: Any] = [
            .font: UIFont.systemFont(ofSize: 14),
            .foregroundColor: member.favColor ?? UIColor.black
        ]

        let nameString = NSMutableAttributedString(string: member.name, attributes: nameAttributes)

        if index % 2 == 0 {
            let emailString = NSAttributedString(string: " (\(member.email))", attributes: [
                .font: UIFont.systemFont(ofSize: 14),
                .foregroundColor: UIColor.darkGray
            ])

            nameString.append(emailString)
        }

        return nameString
    }
```

Question 13
Question 13 of 17

What's your favourite mobile App? Why? How would you improve or change it?
my favourite app is a sri lankan app named "Ikman", i like this app because i am always checking used items to buy such as vehicles, mobile phones and electronic items.

i would like to change the search process and the UI if i get a chance to develop this app.

Question 14
Question 14 of 17

Given the following functions:

func getThingFromSlowService() -> Thing

fund display(_ thing: Thing)

Write a function that calls getThingFromSlowService () on a background thread, and then calls displayThing () on the main thread passing in the return value from getThingFromSlowService().
```swift
func fetchDataAndDisplay() {
   DispatchQueue.global(qos: .background).async { [weak self] in
    guard let self = self else { return }
       let value = self.getThingFromSlowService()
       
       DispatchQueue.main.async {
          display(value)
        }
    }
}

```
Question 15
Question 15 of 17

Given the following functions that asynchronously return Int structs. 

func service1() async throws -> Int

func service2() async throws -> Int

func service3() async throws -> Int

Write a function that adds all the integers and displays the result in the main queue when all services complete.
```swift
func addAllServices() {
    let result1 = Task { try await service1() }
    let result2 = Task { try await service2() }
    let result3 = Task { try await service3() }
    
    await Task.awaitAll(result1, result2, result3)
    
    let sum = result1 + result2 + result3
    
    await DispatchQueue.main.async {
        print("Sum of all services: \(sum)")
    }
}
```

Question 16
Question 16 of 17

Write a Swift implementation of a UITableViewController that presents a UITableView that has one section and four cells.

Each cell should display the name of one of your favorite books, with the name of the author beneath it.

Tapping a cell should present an alert giving the Author's name with either his birthdate or one of his quotes that you really like.

Assume that your controller will NOT be instantiated from a xib file or storyboard.
```swift
class BookTableViewController: UITableViewController {
    
    let books = [
        ("Book 1", "Author 1", "Author 1 Birthdate or Quote"),
        ("Book 2", "Author 2", "Author 2 Birthdate or Quote"),
        ("Book 3", "Author 3", "Author 3 Birthdate or Quote"),
        ("Book 4", "Author 4", "Author 4 Birthdate or Quote")
    ]

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Register cell class
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Cell")
    }

    // MARK: - Table view data source

    override func numberOfSections(in tableView: UITableView) -> Int {
        return 1
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return books.count
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "Cell", for: indexPath)
        
        // Configure the cell
        let (book, author, _) = books[indexPath.row]
        cell.textLabel?.text = book
        cell.detailTextLabel?.text = author

        return cell
    }
    
    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: true)
        
        // Display an alert with author's information
        let (_, author, info) = books[indexPath.row]
        let alert = UIAlertController(title: author, message: info, preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
        present(alert, animated: true, completion: nil)
    }
}
```

Question 17
Question 17 of 17

Complete the implementation below. 

public enum HTTPMethod<T: Codable> {
  case get(T)
  case post(T)
  case patch(T)
  case put(T)
  case delete(T)  
}

func networkResult<Request: Codable, Response: Codable, Result>(endPoint: URL, method: HTTPMethod<Request> = .get, type: Request.Type, subject: @escaping (Response) -> Result) async throws -> Result {
  
  //guard let urlRequest = request(endPoint: endPoint, params: params, method: method) else { throw Error() }
  let (data, response) = try await URLSession.shared.data(for: urlRequest)
  guard let response = response as? HTTPURLResponse else { throw Error(code: ErrorCode.unknown) }
  
  // If HTTP response status code is 200 or 204, decode the JSON response and fulfilled the promise
  // else if HTTP response status code is 4xx, decode the JSON body of the error response and reject the promise with an error
  <your-code-goes-here>
  
  throw Error(code: ErrorCode.unknown)
}
```swift
func networkResult<Request: Codable, Response: Codable, Result>(endPoint: URL, method: HTTPMethod<Request> = .get, type: Request.Type, subject: @escaping (Response) -> Result) async throws -> Result {
  
  //guard let urlRequest = request(endPoint: endPoint, params: params, method: method) else { throw Error() }
  let (data, response) = try await URLSession.shared.data(for: urlRequest)
  guard let response = response as? HTTPURLResponse else { throw Error(code: ErrorCode.unknown) }
  
  // If HTTP response status code is 200 or 204, decode the JSON response and fulfilled the promise
  // else if HTTP response status code is 4xx, decode the JSON body of the error response and reject the promise with an error
   if httpResponse.statusCode == 200 || httpResponse.statusCode == 204 {
        let decodedResponse = try JSONDecoder().decode(Response.self, from: data)
        return subject(decodedResponse)
    } else if (400...499).contains(httpResponse.statusCode) {
        let errorResponse = try JSONDecoder().decode(ErrorResponse.self, from: data)
        throw Error(code: ErrorCode(rawValue: httpResponse.statusCode) ?? ErrorCode.unknown)
    }
  
  throw Error(code: ErrorCode.unknown)
}
```

