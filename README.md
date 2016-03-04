#### awleaswift2prog
#####6
Unowned vs weak  

The big difference between unowned and weak is that unowned is assumed to always have a value.  
weak sets your variable to nil after it has been deallocated, unowned does not.  
```
var a:Int32 = 2_147_483_647
a &+ 1 // -2,147,483,648
var a:UInt8 = 0
a &- 1 // 255
```

verrride postfix operator:
```swift
postfix func ++ (inout a:Ingredient) -> Ingredient {
    a.quantity += 1
    return a
}
var someGin = Ingredient(quantity: 2.5, type: .Gin)
someGin++
```

collection of protocal type
```swift
import UIKit
protocol Powered {
    var on:Bool { get set }
    func turnOn()
    func turnOff()
}
protocol Audible {
    var volume:Float { get set }
    func volumeUp()
    func volumeDown()
}
class Speaker:NSObject, Powered,Audible {
    var on:Bool = false
    var volume:Float = 0.0
    var maxVolume:Float = 10.0

    func desc() -> String {
        return "Speaker: volume \(self.volume)"
    }

    func turnOn() {
        if on {
            print("already on")
        }
        on = true
        print("Powered on")
    }
    func turnOff() {
        if !on {
            print("already off")
        }
        on = false
        volume = 0.0
        print("Powered off")
    }
    func volumeUp() {
        if volume < maxVolume {
            volume += 0.5
        }
        print("Volume turned up to \(volume)")
    }
    func volumeDown() {
        if volume > 0 {
            volume -= 0.5
        }
        print("Volume turned down to \(volume)")
    }
}
var speakers:[protocol<Powered,Audible>] = []
for n in 1...10 {
    speakers.append(Speaker())
}
func turnUpAllSpeakers() {
    for speaker in speakers {
        turnUpSpeaker(speaker)
    }
}
func turnDownAllSpeakers() {
    for speaker in speakers {
        turnDownSpeaker(speaker)
    }
}
func turnUpSpeaker(speaker:protocol<Powered,Audible>) {
    if !speaker.on {
        speaker.turnOn()
    }
    speaker.volumeUp()
    print(speaker)
}
func turnDownSpeaker(speaker:protocol<Powered,Audible>) {
    if !speaker.on {
        speaker.turnOn()
    }
    speaker.volumeDown()
    print(speaker)
}
turnUpAllSpeakers()
```
