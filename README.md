//
//  Queue.swift
//  CustomeQueue
//
//  Created by Sushil Kumar Singh on 03/07/21.
//

import UIKit
// should be an inner class of Queue, but inner classes and generics crash the compiler, SourceKit (repeatedly) and occasionally XCode.
class QueueItem<T> {
    let value:T?
    var next:QueueItem? = nil
    init(newValue:T?) {
        self.value = newValue
    }
}
///
/// A standard queue (FIFO - First In First Out). Supports simultaneous adding and removing, but only one item can be added at a time, and only one item can be removed at a time.
///
public class Queue<T>{
    typealias Element = T
    var front:QueueItem<Element>
    var rear:QueueItem<Element>
    init() {
        // Insert dummy item. Will disappear when the first item is added.
        self.rear = QueueItem(newValue: nil)
        self.front = self.rear
    }
    /// Add a new item to the back of the queue.

    func enqueue(newValue:Element){
        let newItems = QueueItem(newValue: newValue)
        rear.next = newItems
        rear = rear.next!
    }
    /// Return and remove the item at the front of the queue.
    func dequeue()->Element?{
        if  front.next != nil {
            let newValue = front.value
            front = front.next!
            return newValue
        }else{
            return nil
        }
    }
    func isEmpty()->Bool {
        return front === rear
    }
}
