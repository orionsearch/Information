# API
Simple public API description using methods and properties declarations. Doing this helps us providing the same features accross a range of different languages and ecosystems.

_API is described in Swift as it is pretty readable and expressive. So, no one needs to know Swift to read the API description_
```swift
class OSRecords {
	init(_ d: [String: Any])
}
class OrionSearch {
    /* Data importing */
    // Data may also be imported using language / ecosystem specific way of managing data (ex: CoreData, ...)
    
    var data: [OSRecords]
    var keys: [String]
    var filters: [String]
    
    init(data: [[String: Any]] = [], keys: [String], filters: [String] = []) // keys should be ordered by priority
    add(data: [[String: Any]])
    add(keys: [String]) // keys will be added after original keys
    add(filters: [String])
    
}
```
