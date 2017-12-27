# KituraRedis

[![Build Status](https://travis-ci.org/IBM-Swift/Kitura-redis.svg?branch=master)](https://travis-ci.org/IBM-Swift/Kitura-redis)

***Swift Redis library***

KituraRedis is a Swift library for interacting with a Redis database using.

It is dependent on the [BlueSocket](https://github.com/IBM-Swift/BlueSocket.git) module.

## Swift version
The latest version of Kitura-redis requires **Swift 4.0.2**. You can download this version of the Swift binaries by following this [link](https://swift.org/download/). Compatibility with other Swift versions is not guaranteed.

## Build:

  - `swift build`

## Running Tests:

This example uses Docker to run Redis detached with the required password defined in Tests/SwiftRedis/password.txt.

  - `docker run -d -p 6379:6379 redis:alpine redis-server --requirepass password123`
  - `swift test`

## Usage:

```swift
import Foundation
import SwiftRedis

let redis = Redis()

redis.connect(host: "localhost", port: 6379) { (redisError: NSError?) in
    if let error = redisError {
        print(error)
    }
    else {
        print("Connected to Redis")
        // set a key
        redis.set("Redis", value: "on Swift") { (result: Bool, redisError: NSError?) in
            if let error = redisError {
                print(error)
            }
            // get the same key
            redis.get("Redis") { (string: RedisString?, redisError: NSError?) in
                if let error = redisError {
                    print(error)
                }
                else if let string = string?.asString {
                    print("Redis \(string)")
                }
            }
        }
    }
}
```
