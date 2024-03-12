**Lab Report 5**

**CSE15L W24
–
Ed Discussion**

**Student1:** I'm implementing an ```insert``` method for a class called ```MyArrayList.java``` and running tests on it.

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

**Student1:** Here are the failure-inducing input

![Image](lab51.png)

![Image](lab52.png)


**Student1:** I have added ```expandCapacity()``` and ```length++``` to make sure that the size will change accordingly based on the input but for some reason, its still not passing.

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
**Student2:** There is something off with your ```for``` or ```if``` statement(s) but I couldn't tell. I looked almost similar to mine.

**TA:** When testing and debugging a method, in this instance for example the ```insert()``` method we should look at boundary cases (testing insert at the beginning, middle, and at the end of the list. Next of, is Index Out of Bounds making sure the correct exceptions are thrown. Correct implementation for insert and the element is inserted at the correct index. It's also extremely important to check the capacity after calling ``insert()```. Lets break it down.

**Boundary cases:** You have the correct implementation to call ```expandCapacity()``` to make sure the capacity is good incase the array list is full.

```
if(length == values.length){
           expandCapacity(length+1);
        }
```

**Index Out of Bounds:** You have the correct implementation to throw ```IndexOutOfBoundsException()``` when the invalid index is inputted

```
if(index < 0 || index > values.length){
           throw new IndexOutOfBoundsException(); 
}
```

**Bugg Detected**: At **length++**, by placing it inside the loop, it was executed in every iteration of the loop. As a result, the length of the list would end up being greater than the actual number of elements inserted, leading to incorrect behavior. Which leads to the two failure-inducing inputs, index out of bounds and the wrong capacity. You should try and  find a better place to put ```length++```.

```
for(index = length; index > 0; index-- ){
            values[index] = values[index-1];
        length++ /* Take another look at this line and try to see where it would correctly be*/
        }
        values[index] = element;
```

**Student1:** Thank you, I have updated the method. And the test seems to be passing, but you did mention other tests that I should include. Would you be able to help me with them too?

```
public void insert(int index, E element){
        if(index < 0 || index > values.length){
           throw new IndexOutOfBoundsException(); 
        }
        if(length == values.length){
           expandCapacity(length+1);
        }
        for(index = length; index > 0; index-- ){
            values[index] = values[index-1];
        }
        values[index] = element;
        length++ /*Changes made based on the suggestion*/
    }
```
Here are the outputs of the tests.

![Image](lab53.png)

**TA**: To test for boundary cases here is an example that you can look at, but you should implement test cases for inserting at the beginning, middle, and the end, emptyList, ...

```
public void testInsertOutOfBounds(){
        assertThrows(IndexOutOfBoundsException.class,()->{
        listDefaultCap.insert(1000, 1);    
    });
        assertEquals(0, listDefaultCap.length);
    };
```

Part 2: Reflection 

The techinical aspect of lab was very eye opening and has allowed me to make major improvements towards my coding skill. Being able to attend these labs, working with my classmates and actually run tests, de bugging and fixing bugs together made me feel like its the closest enviroment I've had so far that remsemblance an actual work place. Where people work as a team, with help of the Ta's aka profensionals. Im just very gratefull for the experience and hoping my future classes are similar in teaching style and working enviroment. 




