**Lab Report 5**

**CSE15L W24
–
Ed Discussion**

Student1 : I'm implementing an ```insert``` method for a class called ```MyArrayList.java``` and running tests on it.

this is my code for ```insert```. I'm currently using ```VS code``` with ```JUnit``` testing.

```
/**
     * Add an element at the specified index
     *
     * @param index   position to insert the element
     * @param element the element to insert
     */
     public void insert(int index, E element){
        if(index < 0 || index > values.length){
           throw new IndexOutOfBoundsException(); 
        }
        if(length == values.length){
           expandCapacity(length+1);
        }
        for(index = length; index > 0; index-- ){
            values[index] = values[index-1];
        length++
        }
        values[index] = element;

    }
```

Student1: Here are the failure-inducing input

![Image](lab51.png)

![Image](lab52.png)


Student1: I have added ```expandCapacity()``` and ```length++``` to make sure that the size will change accordingly based on the input but for some reason, its still not passing.

This are the two ```@Test``` used for testing my ```insert()``` method

```
/**
* Tests Insert method when an element is inserted at the end
*/
@Test
    public void testInsert() {
        listWithInt.insert(0, 10);
        listDefaultCap.insert(0, 10);

        assertArrayEquals("check data", 
        new Integer[]{10, 1, 2, 3, null, null}, listWithInt.values);
        assertEquals("should increment size", 4, listWithInt.length);

        assertArrayEquals("check data", 
        new Integer[]{10, null, null, null, null}, listDefaultCap.values);
        assertEquals("should increment size", 1, listDefaultCap.length);
    }
```

```
@Test
    public void testInsertMultiple(){
        listDefaultCap.insert(0, 1);
        listDefaultCap.insert(0, 2);
        listDefaultCap.insert(0, 3);
        listDefaultCap.insert(0, 4);
        listDefaultCap.insert(0, 5);
        listDefaultCap.insert(0, 6);
        
        assertEquals(1, listDefaultCap.get(5));
        assertEquals(6, listDefaultCap.get(0));
        assertEquals(6, listDefaultCap.length);

    }
```
Student2: There is something off with your ```for``` or ```if``` statement(s) but I couldn't tell. I looked almost similar to mine.

TA's: When testing and debugging a method, in this instance for example the ```insert()``` method we should look at boundary cases (testing insert at the beginning, middle, and at the end of the list. Next of, is Index Out of Bounds making sure the correct exceptions are thrown. Correct implementation for insert and the element is inserted at the correct index. It's also extremely important to check the capacity after calling ``insert()```. Lets break it down.

Boundary cases: You have the correct implementation to call ```expandCapacity()``` to make sure the capacity is good incase the array list is full.

```
if(length == values.length){
           expandCapacity(length+1);
        }
```







