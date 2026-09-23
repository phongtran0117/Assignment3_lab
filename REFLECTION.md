# Reflection

## 1. In LinkedList::deleteFront(), why does it take two separate delete calls instead of one? Name exactly what each one frees, and name the two new calls back in the program responsible for putting them on the heap in the first place.

The first delete, delete doomed->data, gets rid of the value that the node's pointer points too. That value was create when the addfront(new int xnum) was called. So when this delete call is called, it first free this value,but doesn't free up the node. Which is where the second delete comes from ,delete doomed, which deletes the node itself. it also deletes its data and next pointer field. One delete isn't enough because each delete only frees up one thing. The node new Node<T> (value) creates a new node that repoints the pointer after it got deleted.

## 2. ArrayList never had a destructor before today. Explain, in your own words, why switching from T data[CAPACITY] to T* data_[CAPACITY] is what made a destructor necessary, and what would happen if you forgot to write one. Would you get a compiler error? Why or why not?

Before, the T data[CAPACITY] stores the actual values inside this arraylist, so when the values went away, the arraylist went with it because its bounded to that address. After switching the array only holds the address and the actual values now live on the heap from new. When the arraylist go away, the values are still stuck on the heap , so we need a destructor to come and free up those memory leaks. This will give us the ability to use that memory again. Without a destructor, the compiler will not tell us about the error because it's still good code, and in C++ it doesn't track memory.

## 3. search() and addFront() both take a T*, but they treat that pointer completely differently. Explain the difference in terms of ownership: which one is allowed to delete what you hand it, and which one is never allowed to?

The search() function acts more as a look at the node and review the node and reports back. It compares the data and doesn't have the ownership to delete the data. While on the other other the addfront() funciton takes the ownerhsip of the pointer that it's given and puts it into the list. therefore the list takes oenershup is deleting it later,

## 4. You swapped LinkedList<T> for ArrayList<T> inside makeList() and reran main.cpp without changing a single line there. What two mechanisms, by name, made that possible?

The two mechanisms are the ADT and virtual functions. List<T> is an abstract data type: it only lists what a list can do  without saying how, and main.cpp only ever talks to a List<T>, never to ArrayList or LinkedList directly. The virtual keyword on those methods makes C++ decide at runtime which version to run based on the real object, so list->print() runs LinkedList's print or ArrayList's print depending on what makeList() created. Since makeList() is the only place either class is named, changing that one line switched the whole program without touching main.

## 5. Pick one keyword from the Key Terms glossary that you either had to add today or wouldn't have thought to add on your own. Describe, in your own words, the smallest example you can think of where leaving it out would cause a real problem.

One keyword from the key terms glossary that I was not familar with is the explicit term. Without knowing this term, yes if i put the code Node<int>* n = new Node<int>(new int(5)) it would still run, but the heap would never get deleted.