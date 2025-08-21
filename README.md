# Garbage Collection and `finalize()` Demo in Java

This repository demonstrates how **Garbage Collection** works in Java and how the **`finalize()` method** is invoked before an object is destroyed by the Garbage Collector (GC).

---

## 📌 What is Garbage Collection?

- Garbage Collection in Java is the process of automatically reclaiming memory occupied by objects that are no longer referenced.
- The JVM runs a **Garbage Collector** to clean up unused objects and free memory.

---

## 📌 What is `finalize()`?

- The `finalize()` method is called **before an object is destroyed** by the Garbage Collector.
- It allows developers to perform cleanup operations (like closing files, releasing resources, etc.).
- However, its execution is **not guaranteed**. Modern Java discourages heavy reliance on `finalize()` and prefers `try-with-resources` or explicit cleanup.

---

## 📝 Code Example

```java
class DemoGC {
    int id;

    DemoGC(int id) {
        this.id = id;
        System.out.println("Object " + id + " created.");
    }

    // finalize() method gets called before object is destroyed
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Finalize called for object " + id);
    }
}

public class GarbageCollectionDemo {
    public static void main(String[] args) {
        // Creating objects
        DemoGC obj1 = new DemoGC(1);
        DemoGC obj2 = new DemoGC(2);

        // Making objects eligible for garbage collection
        obj1 = null;
        obj2 = null;

        // Requesting JVM to run Garbage Collector
        System.out.println("Requesting Garbage Collection...");
        System.gc();  

        // Small delay to let GC finish (for demo purposes)
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("End of main method.");
    }
}
