# API
Simple public API description using methods and properties declarations. Doing this helps us providing the same features accross a range of different languages and ecosystems.

_API is described in Swift as it is pretty readable and expressive. So, no one needs to know Swift to read the API description_
```swift
class OSRecord {
    init(_ d: [String: Any])
    func main(key: String)
    func secondary(key: String)
    func private(keys: [String])
}
class OSQuery {
    var limit: UInt8 = 25 // max 256 results
    init(_ s: String, keys: [String]? = nil, filters: [String]? = nil)
}
class OSDatabase {
	init(options: [String: Any])
	func configure(options: [String: Any]) // tokenize and parse every records
	func add(data: [[String: Any]] = [])
	
	// Database should also have private API to perform basic search (SELECT like), so OrionSearch can access the data
}
class OrionSearch {
    /* Data importing */
    // Data may also be imported using language / ecosystem specific way of managing data (ex: CoreData, ...)
    
    var data: [OSRecord]
    var keys: [String]
    var filters: [String]
    
    init(data: OSDatabse, keys: [String], filters: [String] = []) // keys should be ordered by priority
    func add(keys: [String]) // keys will be added after original keys
    func add(filters: [String])
    
    /* Search */
    enum OSSearchType {
        case normal
	case advanced // machine learning related
    }
    func perform(search: OSQuery, type: OSSearchType = .normal, completion: (OSRecord) -> Void) throws
    
    /* Plugins */
    // this is private, but I want to make sure that you know how plugins work
    typealias OSPlugin = ([[OSRecord]]) -> [OSRecord]
    private var plugins: Array<OSPlugin> = []
    func registerPlugin(_ plugin: OSPlugin)
}
```
