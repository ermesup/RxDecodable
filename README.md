# RxDecodable
https://travis-ci.org/ermesup/RxDecodable.svg?branch=master

# Usage
```swift
struct God: RxDecodable {
    let name: String
    let parents: [God]

    static func decode(j: AnyObject) throws -> God {
        return try God(name: j => "name", parents: j => "parents")
    }
}

let disposableBag = DisposableBag()
let hermes = God.rx_decode(["name": "Hermes",
                            "parents": [
                                ["name": "Zeus", "parents": []],
                                ["name": "Maia", "parents": []]
                            ]])

hermes.subscribeError { e in
    print(e) // Decodable Error
}.addDisposableTo(disposableBag)

hermes.subscribe { g in
    print(g.element?.name) // Hermes
    print(g.element?.parents?.first?.name) // Zeus
    print(g.element?.parents?.last?.name) // Maia
}.addDisposableTo(disposableBag)

```

# Installation

## Cocoapods
```bash
pod 'RxDecodable', '~> 0.0.1'
```
