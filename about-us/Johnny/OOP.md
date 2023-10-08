# Object Oriented Programming (OOP) C++
# Table of content 

## Class keyword
The most remarkable feature of C++ is `class`. Class binds together data and methods that work on data. So `class` is an abstract data type (ADT). The creation of class simply creates a template.
```
class class_name {
    public: 
        data & function; 
    private: 
        data & function; 
    protected: 
        data & function; 
}; <-- `the class declaration must end with a semicolon`
```
## Data and functions mode
* `public`: Data members and functions declared under the public mode can be used inside and outside the class.
* `Protected`: Data member and functions can be used inside the class. The child class which inherit from this class also can access to the data and functions member which are specified as protected.
* `Private`: Data member and functions can only be used inside a class. 
    * Private member data can be accessed by member function!
* *By default, all member data and functions are private!*
## Write source code for a function of a class 
* Access to the public member function using `::` operator.
* Example:
```
class demo {
    private:
        int cx, cy;
    public:
        void input_data(int,int);
};
Type Class   Function name
  |    |       |
void demo::input_data(int x,int y)
{
    cx = x;
    cy = y;
}
void main( )
{
    demo d1;              // Object instance
    d1.input_data(10,40); // Call member function of instance d1
    getch();              // Wait key press
}
``` 
## Array of Object
* `class_name` *array[number_elements]* 
## Passing and returning an Object
* Object can be passed to and returned from a function just like a primitive data type.
* Example:
```
class demo {
    int num;
    public:
        void input(int x) {
            num=x;
        }
        void copy(demo);
        void show( ) {
            cout<<“num=”<<num<<endl;
        }
};
void demo::copy (demo d) {
    num=d.num; // Passing a whole Object 
}
void main() {
    demo d1,d2;
    d1.input(20);
    d2.copy(d1);
    cout<<“Object d1\n”<<endl;
    d1.show( );
    cout<<“Object d2\n”;
    d2.show( );
    getch( );
}
```
## Friend function
* *Keyword*: `friend`
* Make a function as friend of a class and allow that friend function to access protected and private data of that class.
* Friend functions are mostly used where two or more classes want to share a common function
* Call a friend function:
    - `class_name`.*friend_function*
* Declaration:
```
class demo
{
    // friend function declaration
    friend data_type function_name (parameters);
};
data_type function_name (parameters)
//definition
{
    function definition;
}
```
* Call friend function
```
demo.function_name(parameters);
```

