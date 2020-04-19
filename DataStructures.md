## Data Structures

<summary>Data Structures</summary>

- ### Arrays
    - Implement an automatically resizing vector.
    - [ ] Description:
        - [Arrays (video)](https://www.coursera.org/learn/data-structures/lecture/OsBSF/arrays)
        - [UC Berkeley CS61B - Linear and Multi-Dim Arrays (video)](https://archive.org/details/ucberkeley_webcast_Wp8oiO_CZZE) (Start watching from 15m 32s)
        - [Basic Arrays (video)](https://archive.org/details/0102WhatYouShouldKnow/02_04-basicArrays.mp4)
        - [Multi-dim (video)](https://archive.org/details/0102WhatYouShouldKnow/02_05-multidimensionalArrays.mp4)
        - [Dynamic Arrays (video)](https://www.coursera.org/learn/data-structures/lecture/EwbnV/dynamic-arrays)
        - [Jagged Arrays (video)](https://www.youtube.com/watch?v=1jtrQqYpt7g)
        - [Jagged Arrays (video)](https://archive.org/details/0102WhatYouShouldKnow/02_06-jaggedArrays.mp4)
        - [Resizing arrays (video)](https://archive.org/details/0102WhatYouShouldKnow/03_01-resizableArrays.mp4)
    - [ ] Implement a vector (mutable array with automatic resizing):
        - [ ] Practice coding using arrays and pointers, and pointer math to jump to an index instead of using indexing.
        - [ ] new raw data array with allocated memory
            - can allocate int array under the hood, just not use its features
            - start with 16, or if starting number is greater, use power of 2 - 16, 32, 64, 128
        - [ ] size() - number of items
        - [ ] capacity() - number of items it can hold
        - [ ] is_empty()
        - [ ] at(index) - returns item at given index, blows up if index out of bounds
        - [ ] push(item)
        - [ ] insert(index, item) - inserts item at index, shifts that index's value and trailing elements to the right
        - [ ] prepend(item) - can use insert above at index 0
        - [ ] pop() - remove from end, return value
        - [ ] delete(index) - delete item at index, shifting all trailing elements left
        - [ ] remove(item) - looks for value and removes index holding it (even if in multiple places)
        - [ ] find(item) - looks for value and returns first index with that value, -1 if not found
        - [ ] resize(new_capacity) // private function
            - when you reach capacity, resize to double the size
            - when popping an item, if size is 1/4 of capacity, resize to half
    - [ ] Time
        - O(1) to add/remove at end (amortized for allocations for more space), index, or update
        - O(n) to insert/remove elsewhere
    - [ ] Space
        - contiguous in memory, so proximity helps performance
        - space needed = (array capacity, which is >= n) * size of item, but even if 2n, still O(n)

- ### Linked Lists
    - [ ] Description:
        - [ ] [Singly Linked Lists (video)](https://www.coursera.org/learn/data-structures/lecture/kHhgK/singly-linked-lists)
        - [ ] [CS 61B - Linked Lists 1 (video)](https://archive.org/details/ucberkeley_webcast_htzJdKoEmO0)
        - [ ] [CS 61B - Linked Lists 2 (video)](https://archive.org/details/ucberkeley_webcast_-c4I3gFYe3w)
    - [ ] [C Code (video)](https://www.youtube.com/watch?v=QN6FPiD0Gzo)
            - not the whole video, just portions about Node struct and memory allocation.
    - [ ] Linked List vs Arrays:
        - [Core Linked Lists Vs Arrays (video)](https://www.coursera.org/learn/data-structures-optimizing-performance/lecture/rjBs9/core-linked-lists-vs-arrays)
        - [In The Real World Linked Lists Vs Arrays (video)](https://www.coursera.org/learn/data-structures-optimizing-performance/lecture/QUaUd/in-the-real-world-lists-vs-arrays)
    - [ ] [why you should avoid linked lists (video)](https://www.youtube.com/watch?v=YQs6IC-vgmo)
    - [ ] Gotcha: you need pointer to pointer knowledge:
        (for when you pass a pointer to a function that may change the address where that pointer points)
        This page is just to get a grasp on ptr to ptr. I don't recommend this list traversal style. Readability and maintainability suffer due to cleverness.
        - [Pointers to Pointers](https://www.eskimo.com/~scs/cclass/int/sx8.html)
    - [ ] implement (I did with tail pointer & without):
        - [ ] size() - returns number of data elements in list
        - [ ] empty() - bool returns true if empty
        - [ ] value_at(index) - returns the value of the nth item (starting at 0 for first)
        - [ ] push_front(value) - adds an item to the front of the list
        - [ ] pop_front() - remove front item and return its value
        - [ ] push_back(value) - adds an item at the end
        - [ ] pop_back() - removes end item and returns its value
        - [ ] front() - get value of front item
        - [ ] back() - get value of end item
        - [ ] insert(index, value) - insert value at index, so current item at that index is pointed to by new item at index
        - [ ] erase(index) - removes node at given index
        - [ ] value_n_from_end(n) - returns the value of the node at nth position from the end of the list
        - [ ] reverse() - reverses the list
        - [ ] remove_value(value) - removes the first item in the list with this value
    - [ ] Doubly-linked List
        - [Description (video)](https://www.coursera.org/learn/data-structures/lecture/jpGKD/doubly-linked-lists)
        - No need to implement

- ### Stack
    - [ ] [Stacks (video)](https://www.coursera.org/learn/data-structures/lecture/UdKzQ/stacks)
    - [ ] [Using Stacks Last-In First-Out (video)](https://archive.org/details/0102WhatYouShouldKnow/05_01-usingStacksForLast-inFirst-out.mp4)
    - [ ] Will not implement. Implementing with array is trivial.

- ### Queue
    - [ ] [Using Queues First-In First-Out(video)](https://archive.org/details/0102WhatYouShouldKnow/05_03-usingQueuesForFirst-inFirst-out.mp4)
    - [ ] [Queue (video)](https://www.coursera.org/lecture/data-structures/queues-EShpq)
    - [ ] [Circular buffer/FIFO](https://en.wikipedia.org/wiki/Circular_buffer)
    - [ ] [Priority Queues (video)](https://archive.org/details/0102WhatYouShouldKnow/05_04-priorityQueuesAndDeques.mp4)
    - [ ] Implement using linked-list, with tail pointer:
        - enqueue(value) - adds value at position at tail
        - dequeue() - returns value and removes least recently added element (front)
        - empty()
    - [ ] Implement using fixed-sized array:
        - enqueue(value) - adds item at end of available storage
        - dequeue() - returns value and removes least recently added element
        - empty()
        - full()
    - [ ] Cost:
        - a bad implementation using linked list where you enqueue at head and dequeue at tail would be O(n)
            because you'd need the next to last element, causing a full traversal each dequeue
        - enqueue: O(1) (amortized, linked list and array [probing])
        - dequeue: O(1) (linked list and array)
        - empty: O(1) (linked list and array)

- ### Hash table
    - [ ] Videos:
        - [ ] [Hashing with Chaining (video)](https://www.youtube.com/watch?v=0M_kIqhwbFo&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb&index=8)
        - [ ] [Table Doubling, Karp-Rabin (video)](https://www.youtube.com/watch?v=BRO7mVIFt08&index=9&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb)
        - [ ] [Open Addressing, Cryptographic Hashing (video)](https://www.youtube.com/watch?v=rvdJDijO2Ro&index=10&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb)
        - [ ] [PyCon 2010: The Mighty Dictionary (video)](https://www.youtube.com/watch?v=C4Kc8xzcA68)
        - [ ] [(Advanced) Randomization: Universal & Perfect Hashing (video)](https://www.youtube.com/watch?v=z0lJ2k0sl1g&list=PLUl4u3cNGP6317WaSNfmCvGym2ucw3oGp&index=11)
        - [ ] [(Advanced) Perfect hashing (video)](https://www.youtube.com/watch?v=N0COwN14gt0&list=PL2B4EEwhKD-NbwZ4ezj7gyc_3yNrojKM9&index=4)

    - [ ] Online Courses:
        - [ ] [Understanding Hash Functions (video)](https://archive.org/details/0102WhatYouShouldKnow/06_02-understandingHashFunctions.mp4)
        - [ ] [Using Hash Tables (video)](https://archive.org/details/0102WhatYouShouldKnow/06_03-usingHashTables.mp4)
        - [ ] [Supporting Hashing (video)](https://archive.org/details/0102WhatYouShouldKnow/06_04-supportingHashing.mp4)
        - [ ] [Language Support Hash Tables (video)](https://archive.org/details/0102WhatYouShouldKnow/06_05-languageSupportForHashTables.mp4)
        - [ ] [Core Hash Tables (video)](https://www.coursera.org/learn/data-structures-optimizing-performance/lecture/m7UuP/core-hash-tables)
        - [ ] [Data Structures (video)](https://www.coursera.org/learn/data-structures/home/week/3)
        - [ ] [Phone Book Problem (video)](https://www.coursera.org/learn/data-structures/lecture/NYZZP/phone-book-problem)
        - [ ] distributed hash tables:
            - [Instant Uploads And Storage Optimization In Dropbox (video)](https://www.coursera.org/learn/data-structures/lecture/DvaIb/instant-uploads-and-storage-optimization-in-dropbox)
            - [Distributed Hash Tables (video)](https://www.coursera.org/learn/data-structures/lecture/tvH8H/distributed-hash-tables)

    - [ ] implement with array using linear probing
        - hash(k, m) - m is size of hash table
        - add(key, value) - if key already exists, update value
        - exists(key)
        - get(key)
        - remove(key)